---
title: Recipes
description: Common tasks with the VerseDB API, from searching the catalog to syncing a collection.
order: 3
---

**Search and paginate the catalog.** All list endpoints (`/series`, `/issues`, `/creators`, `/characters`, ...) accept `?q=` for search, `limit` (per page), and `page`. Walk `meta.last_page` to paginate. Detail endpoints are `/{id}` (e.g. `/api/v1/series/123`).

**Names in other languages.** Catalog entities carry `name_i18n` (one name per language, keyed by BCP 47 tag, such as `{"ja": {"value": "集英社", "source": "manual", "reading": "しゅうえいしゃ"}}`), `aliases_i18n` (alternative names per language) and `original_locale` (the language the entity is from); a character adds `real_name_i18n`, an issue has `name_i18n` alone and a variant `variant_name_i18n`. `name` and the flat `aliases` stay as stored, a series' `original_name` and `original_language` read from `name_i18n` and `original_locale`, and `Accept-Language` changes nothing. `?languages=ja,ko` keeps only those languages in the maps; on `/series` and `/issues`, `languages` is the series-language filter instead, and the maps come back whole.

**Barcode lookup** (requires the `lookup:barcode` scope). `GET /api/v1/lookup/upc/{upc}` resolves a scanned barcode to a full issue. A `200` is a unique match; `404` means no match; `409` means several issues share that pre-1995 barcode, so pick from the returned `matches` array. `GET /api/v1/lookup/isbn/{isbn}` covers trades and hardcovers, and `GET /api/v1/lookup/code/{code}` takes a Lunar or Universal distributor code (`0126IM0451`, `DC10251016`) with the same `200`/`404`/`409` answers.

**Cover photo lookup.** `POST /api/v1/lookup/cover` takes a photo of a comic cover as a multipart `image` (JPEG, PNG, GIF, BMP or WebP, up to 5 MB) and matches it by image against every cover in the catalog. `clear_match: true` comes with the `issue_id`, and the `variant_id` when the photo settles which of the issue's covers it is; `clear_match: false` lists up to five `candidates` it could be, best first. Each candidate carries the issue as the issues list returns it with `include=series`. Only the image is compared, so nothing is read off a slab label. It has its own limit: 5 a minute and 100 a day (PRO: 15 and 500), and `503` means matching is unavailable, not that nothing matched.

**Sync a collection** (requires the `write:collection` scope). `POST /api/v1/issues/{issue}/collection` adds a copy (condition, grading, price paid), `PATCH` updates it, `DELETE` removes it, and `GET /api/v1/issues/{issue}/collection/check` tells you whether an issue is already owned. `GET /api/v1/user/collections` (with the `read:user` scope) pages through everything. This is the flow [ComicTagger](https://github.com/comictagger/comictagger)-style tools use: scan barcode → look up issue → add to collection.

**Let a member connect your site** (no token to paste). Send the member to `https://versedb.com/connect` with an HTTPS `redirect_uri`, a `state` and a PKCE `code_challenge` (S256); they approve on versedb.com and come back with a single-use `code`, which your server exchanges at `POST /api/v1/connect/token` for a one-year token with `read:public` and `read:showcase`. The steps are under [Connect to VerseDB](connect.md).

**Manage lists** (requires the `write:list` scope). `POST /api/v1/lists` creates a list, `POST /api/v1/lists/{list}/items` adds entries, `PUT .../items/reorder` reorders them. Browse public lists with `GET /api/v1/lists` or the platform-curated `GET /api/v1/lists/system`.
