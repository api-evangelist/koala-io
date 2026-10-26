# Koala (koala-io)

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
