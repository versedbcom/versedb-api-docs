---
title: Rate Limits
description: The hourly and daily request limits for each tier, and what happens when you reach one.
order: 6
---

Two complementary limits apply to reads: an **hourly** cap that bounds burst speed, and a **daily** cap that bounds total volume. Both must be satisfied, and whichever you reach first returns a 429. Search shares the read limits.

| Tier | Read / Search (hourly) | Read / Search (daily) | Write (hourly) |
| --- | --- | --- | --- |
| Free | 300/hr | 4,000/day | 150/hr |
| PRO | 1000/hr | 20,000/day | 500/hr |
| Developers Business | 10,000/hr | 100,000/day | None |
| Developers Scale | 100,000/hr | 1,000,000/day | None |

VerseDB Developers keys read the catalog and look up barcodes; every key of an organization draws on its one allowance. Cover photo lookups (`POST /api/v1/lookup/cover`) have their own limit instead: 5 a minute and 100 a day on Free, 15 a minute and 500 a day on PRO. All callers together share 30 a minute, so a 429 can arrive before your own limit; wait for `Retry-After`.

Exceeding either limit returns an HTTP 429 response with a `Retry-After` header telling you when to retry. The daily cap keeps the API responsive for everyone and prevents dataset mirroring (see [Acceptable Use](acceptable-use.md)), so design integrations to cache and request only what they need rather than walking the full catalog. For handling strategies and best practices, see our [API Support Articles](https://versedb.com/support/api).
