---
title: Official SDKs
description: The TypeScript and Python SDKs for the VerseDB API, and the machine-readable spec they are generated from.
order: 5
---

## TypeScript

```bash
npm install @versedbcom/sdk
```

```typescript
import { VerseDB } from "@versedbcom/sdk";

const verseDB = new VerseDB({ token: "<your-api-token>" });
const series = await verseDB.series.listSeries({ q: "batman", limit: 20 });
```

The SDK is generated from this API's OpenAPI spec: typed models and errors for the full catalog, auth set once on the client, and configurable backoff retries (`retryConfig`). Source, runnable examples, and issue tracker: [github.com/versedbcom/versedb-node](https://github.com/versedbcom/versedb-node) ([npm](https://www.npmjs.com/package/@versedbcom/sdk)).

## Python

```bash
pip install versedb
```

```python
from versedb import AuthenticatedClient
from versedb.api.series import list_series

client = AuthenticatedClient(base_url="https://versedb.com", token="<your-api-token>")
page = list_series.sync(client=client, q="batman", limit=20)
```

Generated from the same spec, with typed models and both sync and async calls (`sync`, `asyncio`) on every endpoint. Requires Python 3.11+. Source and issue tracker: [github.com/versedbcom/versedb-python](https://github.com/versedbcom/versedb-python) ([PyPI](https://pypi.org/project/versedb/)).

## Machine-Readable Spec

The OpenAPI 3.1 spec is at [/api/docs.openapi](https://versedb.com/api/docs.openapi) and a Postman collection at [/api/docs.postman](https://versedb.com/api/docs.postman).
