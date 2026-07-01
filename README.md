# Koala (koala-io)

Koala is a B2B buyer-intent and go-to-market platform that de-anonymizes website and product traffic, identifies the visitors and companies behind it, enriches them with firmographic and contact data (via Clearbit Reveal/Enrich and ZoomInfo), and scores first-party intent so sales teams can act on the accounts showing the strongest signals. Its developer surface is a client-side JavaScript pixel plus an HTTP collection API for server-side identify, event, and account ingestion, with a separate secret-key admin API for GDPR deletion.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/koala-io/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/koala-io/refs/heads/main/apis.yml)

## Tags

- Buyer Intent
- Visitor Identification
- De-anonymization
- Enrichment
- Go-to-Market
- Sales Intelligence
- B2B

## Timestamps

- **Created:** 2026-07-01
- **Modified:** 2026-07-01

## A Note on Koala's API Surface

Koala's documented HTTP API is an **ingestion / collection** API, not a query API. You send data *into* Koala (visitor identifies, events, traits, account data) and consume the resulting identified accounts, enrichment, and intent scores through the Koala app, Slack alerts, webhooks/automations, and warehouse/reverse-ETL integrations (BigQuery, Snowflake, Hightouch, Census). The IP-to-company de-anonymization and person/company enrichment are performed by Koala internally (Clearbit Reveal/Enrich, ZoomInfo); Koala does not publish a public REST endpoint to query enriched records directly. There are two auth models: the Collection/Accounts endpoints use the **public project key in the URL path**, while the Deletion (GDPR) endpoint uses a **secret bearer key**.

## APIs

### Koala Collection (Batch) API

Server-side ingestion endpoint. POST visitor identifies, custom events, and traits to /batch keyed by your workspace public API key. Each request must carry a top-level profile_id or email, is capped at 30 of each payload type, and must send a User-Agent header. Authenticated by public (publishable) project key embedded in the path, not a secret bearer token.

- **Human URL:** [https://getkoala.com/docs/developer-guides/server-side](https://getkoala.com/docs/developer-guides/server-side)
- **Base URL:** `https://api2.getkoala.com/web/projects/{public_api_key}`

#### Tags

- Ingestion
- Identify
- Events
- Batch

#### Properties

- [Documentation](https://getkoala.com/docs/developer-guides/server-side)
- [Documentation](https://getkoala.com/docs/developer-guides/sending-identify)
- [OpenAPI](openapi/koala-io-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/koala-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/koala-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Koala Accounts API

Account-level ingestion at /accounts/batch. Send firmographic traits and account events tied to a company domain (or account_id), with an optional group_id to disambiguate multiple tenants/workspaces mapping to the same domain. Koala auto-creates the account if the domain is new.

- **Human URL:** [https://getkoala.com/docs/developer-guides/server-side](https://getkoala.com/docs/developer-guides/server-side)
- **Base URL:** `https://api2.getkoala.com/web/projects/{public_api_key}`

#### Tags

- Accounts
- Company Traits
- Firmographics

#### Properties

- [Documentation](https://getkoala.com/docs/developer-guides/server-side)
- [OpenAPI](openapi/koala-io-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/koala-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/koala-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Koala SDK Bootstrap API

GET on the project root returns the JSON bootstrap configuration the browser pixel needs to initialize. Used to verify a public key or a custom reverse-proxy install is wired correctly.

- **Human URL:** [https://getkoala.com/docs/sdk/installation](https://getkoala.com/docs/sdk/installation)
- **Base URL:** `https://api2.getkoala.com/web/projects/{public_api_key}`

#### Tags

- Pixel
- SDK
- Bootstrap

#### Properties

- [Documentation](https://getkoala.com/docs/sdk/installation)
- [Documentation](https://getkoala.com/docs/get-started/quick-start)
- [OpenAPI](openapi/koala-io-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Koala Web Pixel (JavaScript SDK)

The client-side pixel loaded from cdn.getkoala.com/v1/{key}/sdk.js. Exposes ko.identify(), ko.track(), ko.qualify(), ko.reset() and autotracks pageviews, form fills, and session time. This is a browser SDK, not a REST resource, and it de-anonymizes traffic client-side into the same collection pipeline as the Batch API.

- **Human URL:** [https://getkoala.com/docs/sdk/installation](https://getkoala.com/docs/sdk/installation)
- **Base URL:** `https://cdn.getkoala.com/v1/{public_api_key}`

#### Tags

- Pixel
- JavaScript
- Autotracking
- Client Side

#### Properties

- [Documentation](https://getkoala.com/docs/sdk/installation)
- [Documentation](https://getkoala.com/docs/sdk/identify)
- [Documentation](https://getkoala.com/docs/sdk/track)
- [Documentation](https://getkoala.com/docs/sdk/autotracking)

### Koala Deletion (GDPR) API

Secret-key admin API for GDPR right-to-erasure. POST a list of up to 50 emails to /deletion-requests to queue a deletion and receive a deletion_request_id; GET /deletion-requests/{id} to poll status and retrieve the deletion receipt. Authenticated with an Authorization Bearer secret (sk_...) API key, unlike the public-key collection endpoints.

- **Human URL:** [https://getkoala.com/docs/developer-guides/gdpr-endpoint](https://getkoala.com/docs/developer-guides/gdpr-endpoint)
- **Base URL:** `https://app.getkoala.com/api/v1`

#### Tags

- GDPR
- Deletion
- Privacy
- Compliance

#### Properties

- [Documentation](https://getkoala.com/docs/developer-guides/gdpr-endpoint)
- [OpenAPI](openapi/koala-io-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/koala-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/koala-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [GitHub Organization](https://github.com/getkoala)
- [LinkedIn](https://www.linkedin.com/company/getkoala)
- [Website](https://getkoala.com)
- [Documentation](https://getkoala.com/docs)
- [Plans](plans/koala-io-plans-pricing.yml)
- [Rate Limits](rate-limits/koala-io-rate-limits.yml)
- [Fin Ops](finops/koala-io-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
