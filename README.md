# Wikimedia Enterprise Postman Collection

The official Postman collection for the Wikimedia Enterprise APIs. Use it to explore the API, try requests, and check responses before you write code.

[![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)](https://www.postman.com/wikimedia-enterprise)

The public workspace is at [postman.com/wikimedia-enterprise](https://www.postman.com/wikimedia-enterprise). This repository holds the same collection as a file, `Wikimedia Enterprise APIs.postman_collection.json` (Postman collection format v2.1), which you can import directly.

## Quick start

1. **Create an account.** [Sign up for a free account](https://dashboard.enterprise.wikimedia.com/signup/) and verify your email.
2. **Get the collection.** Fork it from the [public workspace](https://www.postman.com/wikimedia-enterprise), or import the JSON file from this repository (Postman: **Import**, then choose the file).
3. **Add your credentials to the Postman Vault.** Create two vault secrets, `wmeUsername` and `wmePassword`, with your Wikimedia Enterprise username and password. In the vault's settings, turn on **Enable support in scripts**, and allow the collection when Postman asks.
4. **Send a request.** Open **On-demand > Article Lookup**, set the `articlename` collection variable to an article name such as `NASA`, and send it. The collection logs in for you the first time and keeps your access token fresh after that.

No environment is needed. Tokens are stored in collection variables, and your credentials stay in your local vault.

## How authentication works

The Wikimedia Enterprise APIs use JWT bearer tokens: an access token that lasts 24 hours and a refresh token that lasts 90 days.

A collection-level pre-request script handles this before every request outside the **Authentication** folder:

- With no token yet, it calls `/v1/login` with your vault credentials.
- An hour before the access token expires, it calls `/v1/token-refresh`.
- If a refresh fails, or the refresh token is close to its 90-day limit, it logs in again.
- If your credentials are missing, the request stops with an error that says so. Details of each step are in the Postman Console.

You can also run **Authentication > Login** yourself; it stores the tokens in the same place.

**Upgrading from an earlier version?** Earlier versions kept tokens in an environment. The script removes those old token variables from your active environment the first time it runs, so they can't override the new ones.

**Running outside the Postman app** (Newman or the Postman CLI): the vault isn't available there, so pass `wmeUsername` and `wmePassword` as environment or global variables.

## What's inside

| Folder | What it covers |
| :--- | :--- |
| **Authentication** | Login, token refresh, and the forgot-password flow. |
| **Metadata** | Available projects, languages, namespaces, and project codes. |
| **Snapshot** | Snapshot API: list, inspect, and download project snapshots and their chunks, including Structured Contents snapshots (Beta). |
| **On-demand** | On-demand API: look up the current version of an article, its Structured Contents (Beta), and Wikidata items, properties, and labels (Beta). |
| **Realtime** | Realtime API: streaming article and Wikidata updates, and Realtime Batch hourly files. |

Every request links to its entry in the [API reference](https://enterprise.wikimedia.com/docs/api/). The [OpenAPI definition](https://enterprise.wikimedia.com/docs/api/wme-api.yaml) is the full reference for every endpoint and response field.

## Usage notes

- **Account limits** depend on your account. Check your usage in the [Dashboard](https://dashboard.enterprise.wikimedia.com/).
- **Updates:** we update this collection as the API changes. Re-import the file or pull changes into your fork to get new requests.
- **Status:** current API status is at [status.enterprise.wikimedia.com](https://status.enterprise.wikimedia.com/).

## Contributing

Found a problem or have a suggestion? [Open an issue](https://github.com/wikimedia-enterprise/postman/issues). For questions about your account or the APIs, [contact us](https://enterprise.wikimedia.com/contact/).

## License

GPL-3.0. See [LICENSE](LICENSE). Content returned by the APIs comes from Wikipedia and other Wikimedia projects and is licensed under CC BY-SA 4.0.

Maintained by the Wikimedia Enterprise team at the Wikimedia Foundation.
