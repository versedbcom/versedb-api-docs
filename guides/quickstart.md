---
title: Introduction
description: Create a VerseDB API token and make your first request to the catalog.
order: 1
---

Welcome to the VerseDB API. This documentation provides everything you need to integrate with our comic book database.

This is a **personal collection API**: read the full public catalog and build tools around your own data: collections, lists, pull lists, reading progress. The entire catalog (entities, their relationships, and variants) is free for any authenticated token; PRO adds higher rate limits, unlimited lists, and 500 items per list.

## Quickstart

1. Create a token at [versedb.com/my/apps/custom/create](https://versedb.com/my/apps/custom/create). The default `read:public` scope covers all catalog read endpoints; add `read:user` to read your own profile and library (or `read:showcase` for a display-only view of them without email, location, prices, notes, storage or loans), `lookup:barcode` for barcode lookups, and the `write:*` scopes for collection/list management.
2. Call the API with your token as a Bearer header. The base URL is `https://versedb.com/api/v1`.

```bash
curl -H "Authorization: Bearer $VERSEDB_TOKEN" \
     -H "Accept: application/json" \
     "https://versedb.com/api/v1/series?q=batman&limit=20"
```

List endpoints return a `data` array plus a `meta` object (`current_page`, `last_page`, `per_page`, `total`); request the next page with `?page=2`.

For detailed tutorials and code samples, visit our [API Support Articles](https://versedb.com/support/api).
