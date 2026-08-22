# Wistia (wistia)

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

Wistia is an all-in-one video marketing platform for businesses that combines branded video hosting, webinars, video editing, webcam and screen recording, and deep viewer analytics for B2B marketing teams focused on lead generation, brand control, and content performance. Founded in 2006, Wistia is used by more than 425,000 businesses and integrates with major marketing automation and CRM platforms. Wistia exposes a Data API at https://api.wistia.com/v1 for programmatic access to medias, projects, customizations, accounts, and analytics, with authentication via Bearer Token or HTTP Basic using an API access token.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/wistia/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/wistia/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- Video Hosting
- Video Marketing
- Video Analytics
- Lead Generation
- Webinars
- B2B Marketing

## Timestamps

- **Created:** 2026-05-11
- **Modified:** 2026-05-30

## APIs

### Wistia Data API

REST API providing programmatic access to medias, projects, accounts, customizations, captions, and statistics in a Wistia account. Data is returned in JSON over HTTPS. Authentication uses Bearer Tokens via the Authorization header or HTTP Basic Auth with the API token as the password. Rate limited to 600 requests per minute per account.

- **Human URL:** [https://docs.wistia.com/reference/getting-started-with-the-data-api](https://docs.wistia.com/reference/getting-started-with-the-data-api)
- **Base URL:** `https://api.wistia.com/v1`

#### Tags

- Video
- Media
- Analytics
- Captions
- Projects

#### Properties

- [Documentation](https://docs.wistia.com/reference/getting-started-with-the-data-api)
- [Getting Started](https://docs.wistia.com/docs/making-api-requests)
- [Authentication](https://docs.wistia.com/docs/authenticating-with-oauth2)
- [API Reference](https://docs.wistia.com/reference)
- [Postman Collection](collections/wistia.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wistia.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Wistia Upload API

Endpoint for uploading video files directly to a Wistia account, typically used in conjunction with the Data API to manage uploaded media. Authentication uses the same API access token.

- **Human URL:** [https://docs.wistia.com/reference/upload](https://docs.wistia.com/reference/upload)
- **Base URL:** `https://upload.wistia.com`

#### Tags

- Video Upload
- Media Ingest

#### Properties

- [Documentation](https://docs.wistia.com/reference/upload)
- [Postman Collection](collections/wistia.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wistia.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Wistia Webhooks

Real-time webhook deliveries from Wistia for documented media lifecycle events. Deliveries are HTTP POST with a JSON body and are signed via HMAC-SHA256 using the consumer's configured webhook secret, supplied in the X-Wistia-Signature header. See the linked AsyncAPI 2.6 description for the modeled events and payload shape.

- **Human URL:** [https://docs.wistia.com/docs/webhooks](https://docs.wistia.com/docs/webhooks)
- **Base URL:** `https://docs.wistia.com/docs/webhooks`

#### Tags

- Webhooks
- Events
- Media
- AsyncAPI

#### Properties

- [Documentation](https://docs.wistia.com/docs/webhooks)
- [AsyncAPI](https://raw.githubusercontent.com/api-evangelist/wistia/refs/heads/main/asyncapi/wistia-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/latest)
- [Postman Collection](collections/wistia.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/wistia.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/wistia)
- [Website](https://wistia.com)
- [Documentation](https://docs.wistia.com)
- [Pricing](https://wistia.com/pricing)
- [Sign Up](https://wistia.com/signup)
- [Support](https://wistia.com/support)
- [Developers](https://docs.wistia.com)
- [Blog](https://wistia.com/learn)
- [LinkedIn](https://www.linkedin.com/company/wistia)
- [L L Ms Txt](https://docs.wistia.com/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
