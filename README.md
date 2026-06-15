# Wistia (wistia)

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
