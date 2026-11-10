# VerseDB API docs

The VerseDB API (`https://versedb.com/api/v1`) is a REST API for the VerseDB comic book database: read the full public catalog and build tools around your own data: collections, lists, pull lists, reading progress. Requests are authenticated with a personal access token.

The rendered documentation is at [versedb.com/api/docs](https://versedb.com/api/docs).

## What is in this repository

- `guides/`: the guides shown on the documentation page, written here as Markdown.
- `openapi.json`: the OpenAPI 3.1 spec behind the endpoint reference.
- `postman.json`: a Postman collection of the same endpoints.

`openapi.json` and `postman.json` are generated from the live API every night and are not edited by hand. If an endpoint description, parameter or example is wrong, open an issue rather than a pull request against those files.

## Getting a token

Create a token at [versedb.com/my/apps/custom/create](https://versedb.com/my/apps/custom/create). The default `read:public` scope covers all catalog read endpoints; add `read:user` to read your own profile and library (or `read:showcase` for a display-only view of them without email, location, prices, notes, storage or loans), `lookup:barcode` for barcode lookups, and the `write:*` scopes for collection/list management.

Send it as a Bearer header:

```bash
curl -H "Authorization: Bearer $VERSEDB_TOKEN" \
     -H "Accept: application/json" \
     "https://versedb.com/api/v1/series?q=batman&limit=20"
```

## SDKs

- TypeScript: `npm install @versedbcom/sdk` ([versedbcom/versedb-node](https://github.com/versedbcom/versedb-node))
- Python 3.11+: `pip install versedb` ([versedbcom/versedb-python](https://github.com/versedbcom/versedb-python))

Both are generated from `openapi.json`.

## Contributing

Corrections and additions to the guides are welcome as pull requests. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

The guides are licensed under CC BY 4.0. See [LICENSE](LICENSE).
