# Koala

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

**Areas:** Buyer Intent · Visitor Identification · De-anonymization · Data Enrichment · Go-To-Market · Sales Intelligence · B2B · A2A

## Koala on APIs.io

Everything profiled for Koala is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/koala-io/](https://apis.io/providers/koala-io/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [Koala Web Pixel (JavaScript SDK)](https://apis.io/apis/koala-io/koala-io-web-pixel-sdk/) — The client-side pixel loaded from cdn.getkoala.com/v1/{key}/sdk.js. Exposes ko.identify(), ko.track(), ko.qualify(), ko.reset() and autotracks pageviews,…
- [Koala Accounts API](https://apis.io/apis/koala-io/koala-io-accounts-api/) — Account-level (company) trait and event ingestion.
- [Koala Collection API](https://apis.io/apis/koala-io/koala-io-collection-api/) — Server-side ingestion of visitor identifies, events, and traits.
- [Koala Deletion API](https://apis.io/apis/koala-io/koala-io-deletion-api/) — GDPR right-to-erasure requests and status.
- [Koala SDK API](https://apis.io/apis/koala-io/koala-io-sdk-api/) — Bootstrap configuration used by the client-side pixel.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Koala Io Auto Outbound Webhooks](https://apis.io/asyncapis/koala-io/koala-io-auto-outbound-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [koala-docs](https://apis.io/servers/koala-io/koala-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Koala Io Agentic Access](https://apis.io/agentic-access/koala-io/koala-io-agentic-access/)

#### JSON Schema (2)

The data models the API reads and writes.

- [KoalaAccountBatchRequest](https://apis.io/schemas/koala-io/koala-io-account-batch-request/)
- [KoalaProfileBatchRequest](https://apis.io/schemas/koala-io/koala-io-profile-batch-request/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Koala Io Context](https://apis.io/jsonld/koala-io/koala-io-context/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [Koala API Vocabulary](https://apis.io/vocabularies/koala-io/koala-io-vocabulary/)

#### Examples (4)

Example requests and responses.

- [Koala Io Account Batch Event Example](https://apis.io/examples/koala-io/koala-io-account-batch-event-example/)
- [Koala Io Account Batch Traits Example](https://apis.io/examples/koala-io/koala-io-account-batch-traits-example/)
- [Koala Io Profile Batch Identify Example](https://apis.io/examples/koala-io/koala-io-profile-batch-identify-example/)
- [Koala Io Profile Batch Track Example](https://apis.io/examples/koala-io/koala-io-profile-batch-track-example/)

#### Collections (7)

Postman and Open Collection request collections.

- [Koala API](https://apis.io/collections/koala-io/open-koala-io/)
- [Koala Server-Side Account Ingestion API](https://apis.io/collections/koala-io/open-koala-io-account-ingestion-api/)
- [Koala Accounts API](https://apis.io/collections/koala-io/open-koala-io-accounts-api/)
- [Koala Accounts Collection API](https://apis.io/collections/koala-io/open-koala-io-collection-api/)
- [Koala Accounts Deletion API](https://apis.io/collections/koala-io/open-koala-io-deletion-api/)
- [Koala Server-Side Account Ingestion Profile Ingestion API](https://apis.io/collections/koala-io/open-koala-io-profile-ingestion-api/)
- [Koala Accounts SDK API](https://apis.io/collections/koala-io/open-koala-io-sdk-api/)

#### Overlays (6)

OpenAPI overlays, including conversational phrasing for each operation.

- [Koala Io Account Ingestion Api Overlay](https://apis.io/overlays/koala-io/koala-io-account-ingestion-api-overlay/)
- [Koala Io Accounts Api Overlay](https://apis.io/overlays/koala-io/koala-io-accounts-api-overlay/)
- [Koala Io Collection Api Overlay](https://apis.io/overlays/koala-io/koala-io-collection-api-overlay/)
- [Koala Io Deletion Api Overlay](https://apis.io/overlays/koala-io/koala-io-deletion-api-overlay/)
- [Koala Io Profile Ingestion Api Overlay](https://apis.io/overlays/koala-io/koala-io-profile-ingestion-api-overlay/)
- [Koala Io Sdk Api Overlay](https://apis.io/overlays/koala-io/koala-io-sdk-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Koala — jsonschema rules](https://apis.io/rules/koala-io/koala-io-jsonschema-spectral-rules/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Koala Io Authentication](https://apis.io/security/koala-io/koala-io-authentication/)
- [Koala Io Domain Security](https://apis.io/security/koala-io/koala-io-domain-security/)
- [Koala Io Trust Center](https://apis.io/security/koala-io/koala-io-trust-center/)
- [Koala Io Vulnerability Disclosure](https://apis.io/security/koala-io/koala-io-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Koala Io Plans Pricing](https://apis.io/plans/koala-io/koala-io-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Koala Io Rate Limits](https://apis.io/rate-limits/koala-io/koala-io-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Koala Io Finops](https://apis.io/finops/koala-io/koala-io-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://getkoala.com)
- [Documentation](https://getkoala.com/docs)
- [Getting started](https://getkoala.com/docs/get-started/quick-start)
- [API reference](https://getkoala.com/docs/developer-guides/server-side)
- [Pricing](https://getkoala.com/pricing)
- [Sign up](https://app.getkoala.com/signup)
- [Security](https://getkoala.com/security)
- [Compliance](https://app.vanta.com/koala/trust/tzb87epi5imm1qbxktj0bn)
- [Terms of service](https://getkoala.com/legal/terms)
- [Privacy policy](https://getkoala.com/legal/privacy)
- [GitHub](https://github.com/getkoala)
- [Status](https://koala.instatus.com)

## API Evangelist rating

**Kin Score 63.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 65.8 |
| Contract governance | 28.0 |
| Operational transparency | 60.5 |
| Developer ergonomics | 55.4 |
| Access clarity | 77.6 |

**Agent readiness 40.9** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 30.4** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/koala-io/](https://apis.io/providers/koala-io/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Koala: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/koala-io/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
