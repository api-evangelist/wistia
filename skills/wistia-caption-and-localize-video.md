---
name: wistia-caption-and-localize-video
description: >-
  Make a Wistia video accessible and multilingual — order or upload captions, translate the
  transcript, and purchase a dubbed localization — then track each asynchronous order to
  completion. Use when an agent is asked to caption, translate, or dub video in Wistia.
api: wistia:data-api
generated: '2026-08-14'
method: generated
source: >-
  openapi/wistia-data-api-2026-01-openapi.yml,
  openapi/wistia-data-api-modern-edge-openapi.yml,
  https://docs.wistia.com/changelog/localizations-list,
  https://docs.wistia.com/changelog/media-swap,
  https://docs.wistia.com/docs/webhooks
base: https://api.wistia.com/modern
operations:
  - get-captions           # GET    /captions
  - show-captions-file     # GET    /medias/{mediaHashedId}/captions/{languageCode}
  - create-captions        # POST   /medias/{mediaHashedId}/captions
  - update-captions        # PUT    /medias/{mediaHashedId}/captions/{languageCode}
  - delete-captions        # DELETE /medias/{mediaHashedId}/captions/{languageCode}
  - purchase-captions      # POST   /medias/{mediaHashedId}/captions/purchase
  - translate-media        # POST   /medias/{mediaHashedId}/translate
  - gets-localizations     # GET    /medias/{mediaHashedId}/localizations
  - create-localization    # POST   /medias/{mediaHashedId}/localizations
  - show-localization      # GET    /medias/{mediaHashedId}/localizations/{localizationHashedId}
  - delete-localization    # DELETE /medias/{mediaHashedId}/localizations/{localizationHashedId}
---

# Caption and localize a Wistia video

Operation names are Wistia's own MCP tool names from `x-wistia-mcp-tool-name` in the
published OpenAPI. Everything listed here exists in the `2026-01` stable release.

There are three distinct things here and they are easy to confuse:

| Thing | What it is | Operation |
|---|---|---|
| **Captions** | Timed text in one language, attached to the media | `create-captions`, `purchase-captions` |
| **Translation** | Translating an existing *transcript* into another language | `translate-media` |
| **Localization** | A *dubbed* audio track — new speech, lip-synced, 50+ languages | `create-localization` |

## Before you start

- Base `https://api.wistia.com/modern`, `Authorization: Bearer <token>`, TLS required.
- Reads need **Read all folder and media data**; every write needs
  **Read, update & delete anything**.
- `purchase-captions` and `create-localization` **spend money**. Both are marked in
  Wistia's own MCP annotations as non-idempotent — repeating the call orders again.
  Treat both as human-in-the-loop by default; there is no idempotency key to protect you.

## Steps

1. **See what already exists.**
   `gets-localizations` — `GET /medias/{mediaHashedId}/localizations` — and
   `get-captions` — `GET /captions` — before ordering anything. `purchase-captions`
   returns 422 if captions were already purchased, and the message is the only signal.

2. **Get an existing caption track.**
   `show-captions-file` — `GET /medias/{mediaHashedId}/captions/{languageCode}`.
   `languageCode` is the path key, so one media carries at most one track per language.
   404 here means "captions or video not found" without distinguishing which.

3. **Upload your own captions**, if you already have a file.
   `create-captions` — `POST /medias/{mediaHashedId}/captions`.
   Returns 400 if English captions already exist for the video — check step 1 first.
   Correct an existing track with `update-captions`
   (`PUT /medias/{mediaHashedId}/captions/{languageCode}`) rather than deleting and
   re-creating.

4. **Or order captions from Wistia.**
   `purchase-captions` — `POST /medias/{mediaHashedId}/captions/purchase`.
   This is a paid order. A 422 here returns `{ "message": "..." }` — the only operation in
   the API that uses `message` instead of `error` — meaning the account is not eligible,
   captions were already purchased, or another validation failed.
   Completion is signalled by the `media.transcript_updated` webhook, which also carries
   the transcript ID.

5. **Translate the transcript.**
   `translate-media` — `POST /medias/{mediaHashedId}/translate`.
   Track completion with the `media.translation_created` webhook.

6. **Order a dub.**
   `create-localization` — `POST /medias/{mediaHashedId}/localizations`.
   A dub reuses an existing transcript in the target language if one is available; if not,
   the purchase includes translating the transcript, so ordering the translation first
   (step 5) can change what you pay for.
   Track completion with the `media.localization_created` webhook, then confirm with
   `show-localization` — `GET /medias/{mediaHashedId}/localizations/{localizationHashedId}`.

7. **Clean up** with `delete-captions` or `delete-localization`. Both are annotated
   idempotent by Wistia — deleting something already deleted has no additional effect — so
   these are safe to retry.

## Tracking completion

Caption, translation and dub orders are asynchronous and there is **no polling endpoint**
for them; the signal is a webhook. Configure the relevant events at
`https://my.wistia.com/account/webhooks`, verify the `X-Wistia-Signature` HMAC-SHA256
hexdigest of the raw body against your `secret_key`, deduplicate on the event `uuid`, and
order by `generated_at`. See `asyncapi/wistia-asyncapi.yml`.

## Error handling

401 carries a `code` enum (`unauthorized_credentials`, `account_inactive`,
`unauthorized_scope`, `unauthorized_params`) — the only machine-readable error identifier
in this API. 403 means the account's plan lacks the feature. 429 returns `text/plain` plus
`Retry-After`. See `errors/wistia-problem-types.yml`.
