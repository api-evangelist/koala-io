---
name: Request and verify a Koala GDPR erasure
description: >-
  File a right-to-erasure request for up to 50 email addresses against the Koala
  admin API and poll it to completion, then read the deletion receipt.
api: openapi/koala-io-deletion-api-openapi.yml
operations:
  - createDeletionRequest
  - getDeletionRequest
generated: '2026-08-13'
method: generated
source: >-
  openapi/koala-io-deletion-api-openapi.yml +
  https://getkoala.com/docs/developer-guides/gdpr-endpoint
---

# Request and verify a Koala GDPR erasure

> **This endpoint is currently unreachable.** On 2026-08-13 `app.getkoala.com`
> returned HTTP 530 (Cloudflare error 1016, origin DNS failure) on every path,
> including the host root. Koala shuts down 2026-09-30. If you have an outstanding
> erasure obligation that depends on this API, escalate to `support@getkoala.com`
> rather than waiting on the endpoint. See `lifecycle/koala-io-lifecycle.yml`.

## What you need

A **secret** API key (`sk_...`) created in the Koala app under **Settings → API Keys**.
This is a different credential from the public project key used by the ingestion
endpoints — the public key will not authenticate here.

## Steps

1. **File the request — `createDeletionRequest`**
   `POST https://app.getkoala.com/api/v1/deletion-requests`
   - Header: `Authorization: Bearer sk_...`
   - Body: `{"emails": ["a@example.com", "b@example.com"]}`
   - **At most 50 emails.** Anything past the first 50 is silently ignored — not
     rejected. Chunk your list and file multiple requests.
   - Response: `{"deletion_request_id": "<uuid>"}`. Persist this id; it is the only
     handle you get.

2. **Poll — `getDeletionRequest`**
   `GET https://app.getkoala.com/api/v1/deletion-requests/{deletionRequestId}`
   with the same `Authorization` header. Poll until `status` is `completed`.

3. **Read the receipt.** `deleted_receipt[]` has one entry per email with per-store
   counts: `events`, `metrics`, `page_views`, `form_submissions`, `profiles[]`, `ips[]`,
   `account_associations`, plus the third-party caches Koala held a copy in —
   `clearbit_reveal_cache`, `clearbit_enrichment_cache`, `hubspot_contact_cache`,
   `salesforce_contact_caches`, `outreach_prospect_cache`, `outreach_user_caches`.
   Archive this receipt: it is your evidence of erasure and the only enumeration Koala
   publishes of where a subject's data lived.

## Errors

| Status | Meaning |
|---|---|
| 401 | Missing or invalid secret key, or you sent a public project key |
| 404 | Unknown `deletion_request_id` |
| 530 | Host down (observed 2026-08-13) — not an application error |

## Notes

- There is no list operation. If you lose the `deletion_request_id` you cannot find
  the request again through the API.
- There is no idempotency key. Re-filing the same emails creates a second request.
