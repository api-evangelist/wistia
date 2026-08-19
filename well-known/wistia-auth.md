# Wistia auth.md

You are an agent. This document tells you how to register with Wistia and obtain
an OAuth 2.0 access token so you can call the Wistia API and MCP server on a
user's behalf: discover → register → authorize → use → refresh → revoke. Follow
the steps in order.

Wistia is a standard OAuth 2.0 authorization server: dynamic client registration
([RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591)), authorization code
with PKCE ([RFC 7636](https://datatracker.ietf.org/doc/html/rfc7636)), token
revocation ([RFC 7009](https://datatracker.ietf.org/doc/html/rfc7009)), and
discovery metadata ([RFC 8414](https://datatracker.ietf.org/doc/html/rfc8414) /
[RFC 9728](https://datatracker.ietf.org/doc/html/rfc9728)). There is no separate
agent-only protocol — the OAuth 2.0 flow below is the whole surface.

All OAuth and API endpoints are served from `api.wistia.com`.

## Step 1 — Discover

Fetch the two discovery documents. The `agent_auth` block in the
authorization-server document restates the registration and revocation URLs used
below.

```http
GET https://api.wistia.com/.well-known/oauth-protected-resource
GET https://api.wistia.com/.well-known/oauth-authorization-server
```

The authorization-server metadata lists every endpoint, `grant_types_supported`,
and `scopes_supported` referenced here. Treat that document as authoritative — if
a value below disagrees with it, trust the metadata.

## Step 2 — Pick a method

- **Acting on behalf of a person** (recommended): use the **authorization code +
  PKCE** grant (Step 4a). The user signs in at Wistia and consents; the token
  acts as that user.
- **Acting as the application itself** (machine-to-machine): use the
  **client_credentials** grant (Step 4b), if it appears in
  `grant_types_supported`.

## Step 3 — Register a client (RFC 7591)

Register a client dynamically. `redirect_uris` is required for the
authorization-code flow. Set `token_endpoint_auth_method` to `none` for a public
client (native/SPA agent that cannot keep a secret) — you will then use PKCE and
receive no `client_secret`. Omit it (or send `client_secret_basic`) for a
confidential client and you will receive a `client_secret`.

```http
POST https://api.wistia.com/oauth/register
Content-Type: application/json

{
  "client_name": "Your Agent",
  "redirect_uris": ["https://your-agent.example.com/callback"],
  "scope": "all:read",
  "token_endpoint_auth_method": "none"
}
```

Response (201):

```json
{
  "client_id": "...",
  "client_id_issued_at": 1730000000,
  "client_name": "Your Agent",
  "redirect_uris": ["https://your-agent.example.com/callback"],
  "grant_types": ["authorization_code", "refresh_token", "client_credentials"],
  "response_types": ["code"],
  "token_endpoint_auth_method": "none",
  "scope": "all:read"
}
```

A confidential registration additionally returns a `client_secret`. Registration
is rate limited. Persist the `client_id` (and `client_secret`, if confidential) —
you register once and reuse it.

## Step 4 — Get an access token

### 4a. Authorization code + PKCE (user-delegated)

Generate a PKCE `code_verifier` and its `S256` `code_challenge`, then send the
user to the authorization endpoint:

```http
GET https://api.wistia.com/oauth/authorize?response_type=code
  &client_id=<client_id>
  &redirect_uri=<your redirect_uri>
  &scope=all:read
  &code_challenge=<code_challenge>
  &code_challenge_method=S256
  &state=<opaque>
```

The user signs in and approves. Wistia redirects to your `redirect_uri` with a
`code`. Exchange it:

```http
POST https://api.wistia.com/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=<code>
&redirect_uri=<your redirect_uri>
&client_id=<client_id>
&code_verifier=<code_verifier>
```

Confidential clients authenticate the token request with HTTP Basic
(`client_id:client_secret`), or by sending `client_id` and `client_secret` in
the body, instead of the bare `client_id`.

Response (200):

```json
{
  "access_token": "...",
  "token_type": "Bearer",
  "expires_in": 21600,
  "refresh_token": "...",
  "scope": "all:read"
}
```

### 4b. Client credentials (application identity)

If `client_credentials` is listed in `grant_types_supported`, a confidential
client can obtain a token that acts as itself, with no user present:

```http
POST https://api.wistia.com/oauth/token
Authorization: Basic base64(client_id:client_secret)
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&scope=all:read
```

## Step 5 — Use the access token

Send the token as a bearer credential to the Wistia API and MCP server, both on
`api.wistia.com`:

```http
GET https://api.wistia.com/modern/medias
Authorization: Bearer <access_token>
```

The MCP server endpoint is `https://api.wistia.com/mcp/api` (streamable HTTP) and accepts
the same bearer token.

## Step 6 — Refresh

Access tokens expire (`expires_in` seconds after issuance). Exchange your
`refresh_token` for a new one:

```http
POST https://api.wistia.com/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token
&refresh_token=<refresh_token>
&client_id=<client_id>
```

Confidential clients authenticate this request the same way as the token
exchange (HTTP Basic or `client_secret` in the body).

## Step 7 — Revoke (RFC 7009)

To invalidate a token you hold, POST it to the revocation endpoint,
authenticated as the client the token was issued to: HTTP Basic for
confidential clients, or `client_id` in the body for public clients.

```http
POST https://api.wistia.com/oauth/revoke
Content-Type: application/x-www-form-urlencoded

token=<access_token or refresh_token>
&token_type_hint=access_token
&client_id=<client_id>
```

Responds 200 on success and for unknown tokens; 403 means the request did not
authenticate as the client the token belongs to.

## Scopes

Request the narrowest scope set your task needs. The full list is in
`scopes_supported`; the default is `all:read`.

- `all:read` — Read all data
- `all:delegate_to_contact_permissions` — Read, modify, and delete data on your behalf
- `all:all` — Read, update, and delete anything
- `media:read` — Read all folder and media data
- `media:upload` — Upload videos
- `project:write` — Create, update, delete, copy projects
- `stats:read` — Read detailed stats

## Errors

- `invalid_client_metadata` / `invalid_redirect_uri` at `https://api.wistia.com/oauth/register` —
  fix the registration body (a valid `redirect_uris` is required).
- `invalid_grant` at `https://api.wistia.com/oauth/token` — the code, PKCE verifier, or refresh
  token is expired or already used. Restart at Step 4.
- `invalid_scope` — request only scopes listed in `scopes_supported`.
- `429` on registration or token requests — you are rate limited; back off and
  retry.

Full API reference: https://app.wistia.com/doc/data-api
