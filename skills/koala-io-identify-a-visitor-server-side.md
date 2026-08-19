---
name: Identify a Koala visitor from your backend
description: >-
  Associate an anonymous Koala visitor with a known email address (and optional
  traits) from server-side code, using the workspace public project key.
api: openapi/koala-io-profile-ingestion-api-openapi.yml
operations:
  - sendProfileBatch
generated: '2026-08-13'
method: generated
source: >-
  openapi/koala-io-profile-ingestion-api-openapi.yml +
  https://getkoala.com/docs/developer-guides/server-side +
  conventions/koala-io-conventions.yml
---

# Identify a Koala visitor from your backend

> **Availability check first.** Koala was acquired by Cursor and shuts down
> **2026-09-30**. On 2026-08-13 `api2.getkoala.com` answered every path with
> HTTP 400 `{"error": "Koala ingest suspended"}`. Probe the base URL before
> running this skill; if you get that body, stop — nothing you send is stored.
> See `lifecycle/koala-io-lifecycle.yml`.

## What you need

- The workspace **public** project key (`pk_...`), copied from **Settings → Install**
  in the Koala app. It is not a secret; it goes in the URL path, not a header.
- The visitor's `profile_id` (the `ko_id` cookie value, a UUID v4) **or** their email.

## Steps

1. **Read the anonymous id.** On the inbound request, read the `ko_id` cookie. If it
   is absent, mint a UUID v4 and set `ko_id` on the shared top-level domain
   (`.example.com`) so the browser pixel and your backend agree on the same profile.
2. **Call `sendProfileBatch`** — `POST /batch` on
   `https://api2.getkoala.com/web/projects/{publicApiKey}`.
   - Always send `Content-Type: application/json` **and** `User-Agent`. Without a
     `User-Agent` the request is accepted with 200 and then silently discarded as bot
     traffic — the single most dangerous failure mode in this API.
   - Put `profile_id` and/or `email` at the **top level** of the body. A request with
     neither is a 400.
   - To make the identify visible in the Koala debugger, also include an `identifies`
     array entry with `type: "identify"` and a `traits` object.
3. **Check the response.** Success is `200` with `{"ok": true}`. That means accepted,
   not stored or attributed — there is no read API to confirm.

## Constraints you must respect

- At most **30** `events`, **30** `identifies` and **30** `page_views` per request.
- Every entry in one request must belong to the **same person**.
- There is no `Idempotency-Key` header. Only `events[]` entries carry a `message_id`
  dedupe key; identify calls are **not** deduplicated, so a retried identify is
  reprocessed.

## Errors

| Status | Meaning | Do this |
|---|---|---|
| 400 | No top-level `profile_id`/`email`, malformed body, or over the 30-entry cap | Fix the body; do not retry unchanged |
| 401 | Bad public project key in the path | Re-copy the key from Settings → Install |
| 429 | Throttled | Exponential backoff with jitter, honour `Retry-After` |
| 400 `{"error":"Koala ingest suspended"}` | Product wind-down, not your payload | Stop. This is terminal. |

Error bodies are flat `{"error": "...", "code": "..."}` JSON — **not** RFC 9457
problem+json. See `errors/koala-io-problem-types.yml`.
