---
name: Send Koala account traits and events
description: >-
  Attach company-level traits and events to a Koala Account, keyed by domain, using
  the account batch ingestion endpoint.
api: openapi/koala-io-account-ingestion-api-openapi.yml
operations:
  - sendAccountBatch
generated: '2026-08-13'
method: generated
source: >-
  openapi/koala-io-account-ingestion-api-openapi.yml +
  https://getkoala.com/docs/developer-guides/server-side +
  data-model/koala-io-data-model.yml
---

# Send Koala account traits and events

> **Availability check first.** Koala shuts down **2026-09-30** (acquired by Cursor).
> On 2026-08-13 the ingest host returned HTTP 400
> `{"error": "Koala ingest suspended"}` on every path. See
> `lifecycle/koala-io-lifecycle.yml`.

## When to use this instead of the profile batch

Use `sendAccountBatch` when the fact belongs to a **company**, not a person — plan
tier, seat count, contract value, workspace-created events. Account traits become
visible to every visitor Koala has associated with that domain.

## Steps

1. **Choose the account key.** Prefer `domain` (e.g. `getkoala.com`); `account_id` is
   the alternative. One of the two must be at the **top level** of the body or you get
   a 400. Koala auto-creates the Account if the domain has never been seen.
2. **Call `sendAccountBatch`** — `POST /accounts/batch` on
   `https://api2.getkoala.com/web/projects/{publicApiKey}`.
   - Headers: `Content-Type: application/json` and `User-Agent` (mandatory in practice
     — a missing `User-Agent` gets a 200 and a silent drop).
   - `identifies[]` entries carry `type: "identify"` and a `traits` object.
   - `events[]` entries carry `type: "track"`, an `event` name, `properties`, `sent_at`
     and a `message_id`.
3. **Disambiguate multiple tenants of one company** by putting a `group_id` key inside
   the `traits` object. Koala groups traits by `group_id` on the Account page, so a
   customer's dev workspace and marketing workspace do not overwrite each other.
4. **Check the response.** `200` `{"ok": true}` = accepted for processing.

## Constraints

- 30 `events` and 30 `identifies` maximum per request.
- `page_views` do **not** exist on the account batch — profiles only.
- `message_id` on each event is the only idempotency key. Set it to something stable
  and unique (a UUID) so retries do not double-count. Account **traits** have no
  dedupe key, so a replayed identify simply overwrites.

## Errors

`400` missing `domain`/`account_id` or malformed payload · `401` bad public project
key · `429` throttled. Envelope is flat `{"error","code"}` JSON, not RFC 9457. Full
catalog in `errors/koala-io-problem-types.yml`.
