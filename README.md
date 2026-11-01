# Wistia

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Wistia is an all-in-one video marketing platform for businesses that combines branded video hosting, webinars, video editing, webcam and screen recording, and deep viewer analytics for B2B marketing teams focused on lead generation, brand control, and content performance. Founded in 2006, Wistia is used by more than 425,000 businesses and integrates with major marketing automation and CRM platforms. Wistia ships an unusually complete developer surface for its category: a frozen evergreen Data API at https://api.wistia.com/v1 alongside a header-versioned modern API at https://api.wistia.com/modern with dated stable releases (2026-01), OpenAPI 3.1 descriptions made discoverable through an RFC 9727 api-catalog linkset, OAuth 2.0 with RFC 8414/9728 discovery and dynamic client registration, a hosted MCP server at https://api.wistia.com/mcp/api, a Go CLI, a Speakeasy-generated TypeScript SDK, and the Aurora `<wistia-player>` web component.

**Areas:** Video Hosting · Video Marketing · Video Analytics · Lead Generation · Webinars · B2B Marketing · Video Captions · Localization · MCP · Media Management

## Wistia on APIs.io

Everything profiled for Wistia is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/wistia/](https://apis.io/providers/wistia/)** — or go straight to one of the APIs or properties below.

### APIs (49)

- [Wistia MCP Server](https://apis.io/apis/wistia/mcp/) — Wistia's first-party hosted Model Context Protocol server, exposing 125 tools across the media, folders, channels, captions, customizations, tags, webinars,…
- [Wistia Upload API](https://apis.io/apis/wistia/upload-api/) — Endpoint for uploading video files directly to a Wistia account, typically used in conjunction with the Data API to manage uploaded media. Authentication…
- [Wistia Webhooks](https://apis.io/apis/wistia/webhooks/) — Real-time webhook deliveries from Wistia for documented media lifecycle events. Deliveries are HTTP POST with a JSON body and are signed via HMAC-SHA256…
- [Wistia Account API](https://apis.io/apis/wistia/wistia-account-api/) — The Account API from Wistia — 1 operation(s) for account.
- [Wistia Captions API](https://apis.io/apis/wistia/wistia-captions-api/) — The Captions API from Wistia — 3 operation(s) for captions.
- [Wistia Channels API](https://apis.io/apis/wistia/wistia-channels-api/) — The Channels API from Wistia — 2 operation(s) for channels.
- [Wistia Customizations API](https://apis.io/apis/wistia/wistia-customizations-api/) — The Customizations API from Wistia — 1 operation(s) for customizations.
- [Wistia Folders API](https://apis.io/apis/wistia/wistia-folders-api/) — The Folders API from Wistia — 3 operation(s) for folders.
- [Wistia Medias API](https://apis.io/apis/wistia/wistia-medias-api/) — The Medias API from Wistia — 8 operation(s) for medias.
- [Wistia Tags API](https://apis.io/apis/wistia/wistia-tags-api/) — The Tags API from Wistia — 3 operation(s) for tags.
- [Wistia Tokens API](https://apis.io/apis/wistia/wistia-tokens-api/) — The Tokens API from Wistia — 1 operation(s) for tokens.
- [Wistia Webinars API](https://apis.io/apis/wistia/wistia-webinars-api/) — The Webinars API from Wistia — 3 operation(s) for webinars.
- [Wistia Allowed Domains API](https://apis.io/apis/wistia/wistia-allowed-domains-api/) — The Allowed Domains API from Wistia — 2 operation(s) for allowed domains.
- [Wistia Analytics:Account API](https://apis.io/apis/wistia/wistia-analytics-account-api/) — The Analytics:Account API from Wistia — 4 operation(s) for analytics:account.
- [Wistia Analytics:Media API](https://apis.io/apis/wistia/wistia-analytics-media-api/) — The Analytics:Media API from Wistia — 7 operation(s) for analytics:media.
- [Wistia Analytics:Webinar API](https://apis.io/apis/wistia/wistia-analytics-webinar-api/) — The Analytics:Webinar API from Wistia — 5 operation(s) for analytics:webinar.
- [Wistia Background Job Status API](https://apis.io/apis/wistia/wistia-background-job-status-api/) — The Background Job Status API from Wistia — 1 operation(s) for background job status.
- [Wistia Brands API](https://apis.io/apis/wistia/wistia-brands-api/) — The Brands API from Wistia — 1 operation(s) for brands.
- [Wistia Bulk Actions API](https://apis.io/apis/wistia/wistia-bulk-actions-api/) — The Bulk Actions API from Wistia — 1 operation(s) for bulk actions.
- [Wistia Channel Collaborators API](https://apis.io/apis/wistia/wistia-channel-collaborators-api/) — The Channel Collaborators API from Wistia — 2 operation(s) for channel collaborators.
- [Wistia Channel Episodes API](https://apis.io/apis/wistia/wistia-channel-episodes-api/) — The Channel Episodes API from Wistia — 6 operation(s) for channel episodes.
- [Wistia Custom Metadata Field Definitions API](https://apis.io/apis/wistia/wistia-custom-metadata-field-definitions-api/) — The Custom Metadata Field Definitions API from Wistia — 3 operation(s) for custom metadata field definitions.
- [Wistia Custom Metadata Field Values API](https://apis.io/apis/wistia/wistia-custom-metadata-field-values-api/) — The Custom Metadata Field Values API from Wistia — 2 operation(s) for custom metadata field values.
- [Wistia Deleted Media API](https://apis.io/apis/wistia/wistia-deleted-media-api/) — The Deleted Media API from Wistia — 2 operation(s) for deleted media.
- [Wistia Expiring Access Tokens API](https://apis.io/apis/wistia/wistia-expiring-access-tokens-api/) — The Expiring Access Tokens API from Wistia — 1 operation(s) for expiring access tokens.
- [Wistia Extended Audio Descriptions API](https://apis.io/apis/wistia/wistia-extended-audio-descriptions-api/) — The Extended Audio Descriptions API from Wistia — 4 operation(s) for extended audio descriptions.
- [Wistia Folder Sharings API](https://apis.io/apis/wistia/wistia-folder-sharings-api/) — The Folder Sharings API from Wistia — 2 operation(s) for folder sharings.
- [Wistia Live Stream Event Registrations API](https://apis.io/apis/wistia/wistia-live-stream-event-registrations-api/) — The Live Stream Event Registrations API from Wistia — 1 operation(s) for live stream event registrations.
- [Wistia Live Stream Events API](https://apis.io/apis/wistia/wistia-live-stream-events-api/) — The Live Stream Events API from Wistia — 2 operation(s) for live stream events.
- [Wistia Localizations API](https://apis.io/apis/wistia/wistia-localizations-api/) — The Localizations API from Wistia — 2 operation(s) for localizations.
- [Wistia Media API](https://apis.io/apis/wistia/wistia-media-api/) — The Media API from Wistia — 11 operation(s) for media.
- [Wistia Project Sharings API](https://apis.io/apis/wistia/wistia-project-sharings-api/) — The Project Sharings API from Wistia — 2 operation(s) for project sharings.
- [Wistia Projects API](https://apis.io/apis/wistia/wistia-projects-api/) — The Projects API from Wistia — 3 operation(s) for projects.
- [Wistia Push Devices API](https://apis.io/apis/wistia/wistia-push-devices-api/) — The Push Devices API from Wistia — 2 operation(s) for push devices.
- [Wistia Remix API](https://apis.io/apis/wistia/wistia-remix-api/) — The Remix API from Wistia — 5 operation(s) for remix.
- [Wistia Resource URLs API](https://apis.io/apis/wistia/wistia-resource-urls-api/) — The Resource URLs API from Wistia — 1 operation(s) for resource urls.
- [Wistia Review Bundles API](https://apis.io/apis/wistia/wistia-review-bundles-api/) — The Review Bundles API from Wistia — 2 operation(s) for review bundles.
- [Wistia Search API](https://apis.io/apis/wistia/wistia-search-api/) — The Search API from Wistia — 1 operation(s) for search.
- [Wistia Share Links API](https://apis.io/apis/wistia/wistia-share-links-api/) — The Share Links API from Wistia — 2 operation(s) for share links.
- [Wistia Stats:Account API](https://apis.io/apis/wistia/wistia-stats-account-api/) — The Stats:Account API from Wistia — 2 operation(s) for stats:account.
- [Wistia Stats:Events API](https://apis.io/apis/wistia/wistia-stats-events-api/) — The Stats:Events API from Wistia — 2 operation(s) for stats:events.
- [Wistia Stats:Media API](https://apis.io/apis/wistia/wistia-stats-media-api/) — The Stats:Media API from Wistia — 3 operation(s) for stats:media.
- [Wistia Stats:Projects API](https://apis.io/apis/wistia/wistia-stats-projects-api/) — The Stats:Projects API from Wistia — 1 operation(s) for stats:projects.
- [Wistia Stats:Visitors API](https://apis.io/apis/wistia/wistia-stats-visitors-api/) — The Stats:Visitors API from Wistia — 2 operation(s) for stats:visitors.
- [Wistia Taggings API](https://apis.io/apis/wistia/wistia-taggings-api/) — The Taggings API from Wistia — 1 operation(s) for taggings.
- [Wistia Trims API](https://apis.io/apis/wistia/wistia-trims-api/) — The Trims API from Wistia — 1 operation(s) for trims.
- [Wistia Webinar Collaborators API](https://apis.io/apis/wistia/wistia-webinar-collaborators-api/) — The Webinar Collaborators API from Wistia — 2 operation(s) for webinar collaborators.
- [Wistia Webinar Registrations API](https://apis.io/apis/wistia/wistia-webinar-registrations-api/) — The Webinar Registrations API from Wistia — 1 operation(s) for webinar registrations.
- [Wistia Sub Folders API](https://apis.io/apis/wistia/wistia-sub-folders-api/) — The Sub Folders API from Wistia — 5 operation(s) for sub folders.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (2)

Event-driven and webhook contracts.

- [Wistia Webhooks API](https://apis.io/asyncapis/wistia/wistia-asyncapi/)
- [Wistia Webhooks](https://apis.io/asyncapis/wistia/wistia-webhooks/)

#### Event channels (11)

Individual events and webhooks the provider emits.

- [media.created](https://apis.io/channels/wistia/media-created/)
- [media.deleted](https://apis.io/channels/wistia/media-deleted/)
- [media.failed](https://apis.io/channels/wistia/media-failed/)
- [media.localization_created](https://apis.io/channels/wistia/media-localization-created/)
- [media.localization_failed](https://apis.io/channels/wistia/media-localization-failed/)
- [media.processing](https://apis.io/channels/wistia/media-processing/)
- [media.ready](https://apis.io/channels/wistia/media-ready/)
- [media.transcript_failed](https://apis.io/channels/wistia/media-transcript-failed/)
- [media.transcript_updated](https://apis.io/channels/wistia/media-transcript-updated/)
- [media.translation_created](https://apis.io/channels/wistia/media-translation-created/)
- [media.updated](https://apis.io/channels/wistia/media-updated/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Wistia API MCP Server](https://apis.io/servers/wistia/wistia-api-mcp-server/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Wistia Agentic Access](https://apis.io/agentic-access/wistia/wistia-agentic-access/)

#### Collections (11)

Postman and Open Collection request collections.

- [Wistia Data API](https://apis.io/collections/wistia/open-wistia/)
- [Wistia Data Account API](https://apis.io/collections/wistia/open-wistia-account-api/)
- [Wistia Data Account AllowedDomains API](https://apis.io/collections/wistia/open-wistia-alloweddomains-api/)
- [Wistia Data Account Captions API](https://apis.io/collections/wistia/open-wistia-captions-api/)
- [Wistia Data Account Channels API](https://apis.io/collections/wistia/open-wistia-channels-api/)
- [Wistia Data Account Customizations API](https://apis.io/collections/wistia/open-wistia-customizations-api/)
- [Wistia Data Account Folders API](https://apis.io/collections/wistia/open-wistia-folders-api/)
- [Wistia Data Account Medias API](https://apis.io/collections/wistia/open-wistia-medias-api/)
- [Wistia Data Account Tags API](https://apis.io/collections/wistia/open-wistia-tags-api/)
- [Wistia Data Account Tokens API](https://apis.io/collections/wistia/open-wistia-tokens-api/)
- [Wistia Data Account Webinars API](https://apis.io/collections/wistia/open-wistia-webinars-api/)

#### Overlays (47)

OpenAPI overlays, including conversational phrasing for each operation.

- [Wistia Account Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-account-api-phrasing-overlay/)
- [Wistia Allowed Domains Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-allowed-domains-api-phrasing-overlay/)
- [Wistia Analytics Account Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-analytics-account-api-phrasing-overlay/)
- [Wistia Analytics Media Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-analytics-media-api-phrasing-overlay/)
- [Wistia Analytics Webinar Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-analytics-webinar-api-phrasing-overlay/)
- [Wistia Background Job Status Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-background-job-status-api-phrasing-overlay/)
- [Wistia Brands Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-brands-api-phrasing-overlay/)
- [Wistia Bulk Actions Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-bulk-actions-api-phrasing-overlay/)
- [Wistia Captions Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-captions-api-phrasing-overlay/)
- [Wistia Channel Collaborators Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-channel-collaborators-api-phrasing-overlay/)
- [Wistia Channel Episodes Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-channel-episodes-api-phrasing-overlay/)
- [Wistia Channels Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-channels-api-phrasing-overlay/)
- [Wistia Custom Metadata Field Definitions Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-custom-metadata-field-definitions-api-phrasing-overlay/)
- [Wistia Custom Metadata Field Values Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-custom-metadata-field-values-api-phrasing-overlay/)
- [Wistia Customizations Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-customizations-api-phrasing-overlay/)
- [Wistia Data Api 2026 01 Overlay](https://apis.io/overlays/wistia/wistia-data-api-2026-01-overlay/)
- [Wistia Deleted Media Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-deleted-media-api-phrasing-overlay/)
- [Wistia Expiring Access Tokens Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-expiring-access-tokens-api-phrasing-overlay/)
- [Wistia Extended Audio Descriptions Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-extended-audio-descriptions-api-phrasing-overlay/)
- [Wistia Folder Sharings Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-folder-sharings-api-phrasing-overlay/)
- [Wistia Folders Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-folders-api-phrasing-overlay/)
- [Wistia Live Stream Event Registrations Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-live-stream-event-registrations-api-phrasing-overlay/)
- [Wistia Live Stream Events Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-live-stream-events-api-phrasing-overlay/)
- [Wistia Localizations Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-localizations-api-phrasing-overlay/)
- [Wistia Media Api Phrasing Overlay](https://apis.io/overlays/wistia/wistia-media-api-phrasing-overlay/)
- …and 22 more published on APIs.io

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Wistia — asyncapi rules](https://apis.io/rules/wistia/wistia-asyncapi-spectral-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Wistia Authentication](https://apis.io/security/wistia/wistia-authentication/)
- [Wistia Domain Security](https://apis.io/security/wistia/wistia-domain-security/)
- [Wistia Trust Center](https://apis.io/security/wistia/wistia-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Wistia Scopes](https://apis.io/scopes/wistia/wistia-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Wistia Plans Pricing](https://apis.io/plans/wistia/wistia-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Wistia Rate Limits](https://apis.io/rate-limits/wistia/wistia-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://wistia.com)
- [Documentation](https://docs.wistia.com)
- [Getting started](https://docs.wistia.com/docs/making-api-requests)
- [API reference](https://docs.wistia.com/reference)
- [Pricing](https://wistia.com/pricing)
- [Support](https://wistia.com/support)
- [Blog](https://wistia.com/learn)
- [Compliance](https://security.wistia.com/)
- [Terms of service](https://wistia.com/terms)
- [Privacy policy](https://wistia.com/privacy)
- [GitHub](https://github.com/wistia)
- [Status](https://status.wistia.com)

## API Evangelist rating

**Kin Score 69.9** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 64.0 |
| Contract governance | 29.5 |
| Operational transparency | 69.7 |
| Developer ergonomics | 54.2 |
| Access clarity | 92.1 |

**Agent readiness 35.7** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | — |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/wistia/](https://apis.io/providers/wistia/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Wistia: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/wistia/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
