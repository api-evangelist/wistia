---
name: wistia-run-a-webinar
description: >-
  Create a Wistia webinar, register attendees through the API, and read registration and
  attendance analytics afterwards. Use when an agent is asked to schedule a webinar, push
  registrations from another system, or report on webinar performance.
api: wistia:data-api
generated: '2026-08-14'
method: generated
source: >-
  openapi/wistia-data-api-2026-01-openapi.yml,
  openapi/wistia-data-api-modern-edge-openapi.yml,
  https://docs.wistia.com/reference/post_webinars-webinarid-registrations,
  https://docs.wistia.com/docs/use-webinar-embeds-with-api-registrations
base: https://api.wistia.com/modern
operations:
  - get-webinars                  # GET    /webinars
  - create-webinar                # POST   /webinars
  - update-webinar                # PUT    /webinars/{id}
  - delete-webinar                # DELETE /webinars/{id}
  - create-webinar-registration   # POST   /webinars/{webinarId}/registrations
  - list-webinar-registrations    # GET    /webinars/{webinarId}/registrations  (edge only)
  - create-webinar-collaborator   # POST   /webinars/{webinarId}/collaborators  (edge only)
---

# Run a webinar through the Wistia API

Operation names are Wistia's own MCP tool names from `x-wistia-mcp-tool-name`. Operations
marked **edge only** exist in the edge description but not in the `2026-01` stable release —
they will not resolve against a pinned `X-Wistia-Api-Version: 2026-01`.

Webinars were called **live stream events** in v1. `/v1/live_stream_events` became
`/modern/webinars` and `/v1/live_stream_event_registrations` became
`/modern/webinar_registrations` in the `2026-01` release.

## Before you start

- Base `https://api.wistia.com/modern`, `Authorization: Bearer <token>`, TLS required.
- Every write needs **Read, update & delete anything**.
- **Webinars are plan-gated.** Five operations in this flow declare a 403 whose published
  message is `Webinars are not available on your current plan`. That is an account
  capability gap: the token is valid, retrying will not help, and re-authorizing will not
  help. Surface it to a human as a billing question, not an auth failure.
- Webinars are addressed by a plain numeric `id`, not a hashed id — unlike media and
  channels. Do not reuse hashed-id handling here.

## Steps

1. **Check the account can host webinars.**
   `get-webinars` — `GET /webinars`. A 403 here ends the flow: the plan does not include
   webinars. Everything downstream will fail the same way.

2. **Create the webinar.**
   `create-webinar` — `POST /webinars`.
   422 returns `{ "errors": [ ... ] }` — an array, not a string — with published examples
   `Title is required` and `Event duration must be at least 15 minutes`. Validate duration
   client-side before calling.
   There is no idempotency key: a timed-out create may have succeeded. Re-list with
   `get-webinars` before retrying, or you will create a duplicate event.

3. **Adjust it.**
   `update-webinar` — `PUT /webinars/{id}`. A full state-setter, so it is safe to replay.

4. **Add collaborators.** *(edge only)*
   `create-webinar-collaborator` — `POST /webinars/{webinarId}/collaborators`.

5. **Register attendees.**
   `create-webinar-registration` — `POST /webinars/{webinarId}/registrations` with the
   registrant's email, first name and last name.
   This returns a **unique visitor key and a personalized webinar URL** for that registrant —
   that URL is the deliverable. Send it to the registrant; it is what ties their attendance
   back to analytics.
   Registering the same email twice is not de-duplicated by an idempotency key, so keep
   your own record of who you have already registered.

6. **Read back the roster.** *(edge only)*
   `list-webinar-registrations` — `GET /webinars/{webinarId}/registrations`.

7. **Report on it.**
   The edge description carries an `Analytics:Webinar` surface, including
   `GET /analytics/webinars/{webinarId}/registration`, which returns a registration
   timeseries with configurable granularity — impressions, registrations and completion
   rates per bucket. The `start_date`/`end_date` range must not exceed two years, and it
   requires the **Read detailed stats** token permission.

8. **Tear down.**
   `delete-webinar` — `DELETE /webinars/{id}`. Destructive. Wistia annotates deletes as
   idempotent, so a retry after a timeout is safe.

## Embedding

If registration is happening through an embedded form rather than the API, see
`https://docs.wistia.com/docs/use-webinar-embeds-with-api-registrations` and
`https://docs.wistia.com/docs/embed-webinars-with-tag-managers-and-cookie-consent` — the
tag-manager and cookie-consent path is where webinar embed tracking most often goes silent.

## Error handling

- **403** — plan gap, permanent for this account.
- **422** — `{ "errors": [...] }` for webinar create/update; `{ "errors": { "field": [...] } }`
  for registrations. Handle both shapes.
- **500** on webinar creation returns both `error` and `errors` in the same body.
- **429** — `Retry-After` in seconds, `text/plain` body.

See `errors/wistia-problem-types.yml` and `conventions/wistia-conventions.yml`.
