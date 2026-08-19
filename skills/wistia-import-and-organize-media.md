---
name: wistia-import-and-organize-media
description: >-
  Import a video into Wistia from a public URL, wait for the asynchronous job to finish,
  then file it into the right folder, tag it, and set its thumbnail and playback
  customizations. Use when an agent needs to get an existing video into a Wistia library
  and leave it correctly organized, not just uploaded.
api: wistia:data-api
generated: '2026-08-14'
method: generated
source: >-
  openapi/wistia-data-api-modern-edge-openapi.yml,
  openapi/wistia-data-api-2026-01-openapi.yml,
  https://docs.wistia.com/reference/post_medias-import-url,
  https://docs.wistia.com/docs/making-api-requests
base: https://api.wistia.com/modern
operations:
  - import-media-from-url        # POST /medias/import_url        (edge only)
  - show-background-job-status   # GET  /background_job_status/{backgroundJobStatusId}
  - get-folders                  # GET  /folders
  - create-folder                # POST /folders
  - move-media                   # PUT  /medias/move
  - update-media                 # PUT  /medias/{mediaHashedId}
  - bulk-tag-media               # POST /taggings/bulk_create
  - update-thumbnail-customizations  # PUT /medias/{mediaId}/customizations/thumbnail (edge only)
---

# Import and organize media in Wistia

Every operation name below is Wistia's own MCP tool name, taken from
`x-wistia-mcp-tool-name` in the published OpenAPI. Where an operation exists only in the
edge description and not in the `2026-01` stable release, it is marked **edge only** —
calling it against a pinned stable version will fail.

## Before you start

- Base URL is `https://api.wistia.com/modern`. Send
  `X-Wistia-Api-Version: 2026-01` to pin the stable release, or omit it and accept the
  newest release (Wistia recommends pinning).
- Authenticate with `Authorization: Bearer <token>`. TLS is required.
- The token needs the **Read, update & delete anything** permission for every write below.
- Budget: 600 requests per minute account-wide. `PUT /medias/move` has its own much
  tighter ceiling of **10 requests per 5 minutes** — plan bulk moves around that, not
  around the 600.
- There is **no idempotency key**. If a create call times out, do not blindly retry it —
  list first and check whether the resource already exists.

## Steps

1. **Pick or create the destination folder.**
   `get-folders` — `GET /folders` — lists folders (the resource formerly called projects).
   If nothing matches, `create-folder` — `POST /folders`.
   Note the folder's `hashed_id`; most write bodies want `folder_id`, which in the
   `2026-01` release replaced v1's `project_id`.

2. **Import the source video.** *(edge only)*
   `import-media-from-url` — `POST /medias/import_url` with the publicly reachable file
   URL. Wistia's servers fetch the file directly, so a signed or private URL will fail.
   Imports from some domains (vimeo.com, wistia.com) are refused.
   If you omit `folder_id`, Wistia creates a folder named "Untitled Folder" and puts the
   media there — always pass `folder_id` if you care where it lands.
   This returns a `background_job_status` object, **not** a media object.

3. **Poll the job to completion.**
   `show-background-job-status` — `GET /background_job_status/{backgroundJobStatusId}`.
   There is no completion webhook for import, so polling is the only option. Back off
   between polls; a long video consumes your 600/minute budget quickly if you poll tightly.
   The media's `status` field moves through `queued` → processing → ready, and `progress`
   is a float from 0 to 1.

4. **Name and describe it.**
   `update-media` — `PUT /medias/{mediaHashedId}`. Address media by the opaque
   `hashed_id`, not the numeric `id` — the object carries both and passing the wrong one
   returns 404 with no hint about which you got wrong.

5. **Move it if the import landed elsewhere.**
   `move-media` — `PUT /medias/move`, max 100 media per request, returns a background job.
   Pass `subfolder_id` as well as `folder_id` to land it in a subfolder; the subfolder must
   belong to the folder you named.

6. **Tag it.**
   `bulk-tag-media` — `POST /taggings/bulk_create` applies tags to many media in one call.
   Create tags first with `create-tags` — `POST /tags` — if they do not exist; creating a
   tag that already exists returns 422 `Validation failed: Name has already been taken`.

7. **Set the thumbnail.** *(edge only)*
   `update-thumbnail-customizations` — `PUT /medias/{mediaId}/customizations/thumbnail`.
   This is a partial update: only the fields you send change, and sending a field as `null`
   deletes it and reverts to the default. Note this path uses `{mediaId}` while the media
   operations use `{mediaHashedId}` — both take the hashed id.

## Error handling

- **401 with `code: unauthorized_scope`** — the token lacks the permission tier, not the
  wrong token. Re-issue with broader permissions; retrying will not help.
- **403** — the *account* lacks the feature (for example archiving). This is a plan gap,
  permanent for this account. Do not retry and do not re-authorize.
- **422** — validation. The body is sometimes `{ "error": "..." }`, sometimes
  `{ "errors": [...] }`, sometimes `{ "errors": { "field": [...] } }`. Handle all three.
- **429** — read `Retry-After` (seconds) and wait. The body is `text/plain`, not JSON, so
  do not pipe it into a JSON parser.

See `errors/wistia-problem-types.yml` and `conventions/wistia-conventions.yml`.
