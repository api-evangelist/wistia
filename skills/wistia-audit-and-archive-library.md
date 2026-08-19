---
name: wistia-audit-and-archive-library
description: >-
  Walk a Wistia account's folders and media, pull per-media performance, and archive or
  restore videos in bulk based on what the numbers say. Use when an agent is asked to clean
  up a video library, find unused videos, or report on library performance.
api: wistia:data-api
generated: '2026-08-14'
method: generated
source: >-
  openapi/wistia-data-api-2026-01-openapi.yml,
  https://docs.wistia.com/reference/put_medias-archive,
  https://docs.wistia.com/reference/put_medias-move,
  https://docs.wistia.com/docs/making-api-requests
base: https://api.wistia.com/modern
operations:
  - get-current-account          # GET /account
  - get-folders                  # GET /folders
  - get-subfolders               # GET /folders/{folderId}/subfolders
  - get-medias                   # GET /medias
  - show-media-aggregated-stats  # GET /medias/{mediaHashedId}/stats
  - archive-media                # PUT /medias/archive
  - restore-media                # PUT /medias/restore
  - show-background-job-status   # GET /background_job_status/{backgroundJobStatusId}
  - search                       # GET /search
---

# Audit and archive a Wistia library

Operation names are Wistia's own MCP tool names from `x-wistia-mcp-tool-name`. Everything
here exists in the `2026-01` stable release. This flow is read-heavy and rate-limit-bound,
so pagination discipline matters more than anything else.

## Before you start

- Base `https://api.wistia.com/modern`, `Authorization: Bearer <token>`, TLS required.
- Reads need **Read all folder and media data**. Stats need **Read detailed stats** —
  a different tier. A token that lists media fine can 401 on stats.
- **Archiving is destructive and account-gated.** Wistia annotates `archive-media` as
  destructive, and a 403 means the account's plan has no Archiving feature. Webinar media
  and Soapbox videos imported before 2023-09-01 cannot be archived at all.
- Budget: 600 requests/minute account-wide across `api.wistia.com` and
  `upload.wistia.com`. A per-media stats crawl is the expensive part of this flow — one
  request per video.

## Steps

1. **Confirm which account the token belongs to.**
   `get-current-account` — `GET /account`. Do this first. A token can belong to an account
   you did not expect, and every destructive step below is account-wide.

2. **Enumerate the library.**
   `get-folders` — `GET /folders` — then `get-subfolders` —
   `GET /folders/{folderId}/subfolders` — for each folder.
   Page with `page` and `per_page`; `per_page` maxes out at 100, which is also the default.
   There is **no total count and no next link** in the response — it is a bare array, so
   you know you are done only when a page comes back short.
   If the token is scoped `all:delegate_to_contact_permissions`, `get-folders` returns only
   the folders that one contact can see, so an "empty" library may just be a narrow token.

3. **List media.**
   `get-medias` — `GET /medias` — optionally filtered by `folder_id`. Batch-fetch specific
   videos with `hashed_ids[]=abc123&hashed_ids[]=def456`; the singular `hashed_id`
   parameter was **removed** in `2026-01`.
   Sort with `sort_by` (`name`, `created`, `updated`) and `sort_direction`
   (`1` ascending, `0` descending) — sorting by `updated` descending is the cheap way to
   find stale media without pulling stats for everything.

4. **Or search instead of crawling.**
   `search` — `GET /search?q=<query>` — is one request instead of N. It returns 400 if `q`
   is missing, with the message `the "q" parameter should specify the search query`.

5. **Pull performance.**
   `show-media-aggregated-stats` — `GET /medias/{mediaHashedId}/stats` — one call per
   video. This is where you burn your rate budget; throttle to stay under 600/minute and
   cache results rather than re-crawling.

6. **Archive what is dead.**
   `archive-media` — `PUT /medias/archive` — accepts up to **100 media per request** and
   returns a `background_job_status` object rather than media objects.
   Poll with `show-background-job-status` —
   `GET /background_job_status/{backgroundJobStatusId}`.

7. **Undo if needed.**
   `restore-media` — `PUT /medias/restore` — same 100-per-request cap, same background job,
   and requires the account to have the Archiving feature. Wistia annotates both archive
   and restore as idempotent, so a retried batch is safe.

## Rate limits worth planning around

| Operation | Ceiling |
|---|---|
| Everything | 600 requests / minute, per account |
| `PUT /medias/move` | **10 requests / 5 minutes** — a separate, much tighter limit |
| `PUT /medias/archive`, `PUT /medias/restore` | 100 media per request |
| List pagination | 100 results per page |

On 429 read `Retry-After` (seconds). The 429 body is `text/plain`, unlike every other
error in this API. There are **no** `X-RateLimit-*` or `RateLimit-*` headers, so you cannot
see remaining budget — you have to count your own calls. See
`rate-limits/wistia-rate-limits.yml`.

## Safety

Archiving is bulk and destructive and there is no idempotency key. Confirm the media list
with a human before calling `archive-media`, and log the `hashed_id`s you sent so a restore
is possible without re-deriving the set.
