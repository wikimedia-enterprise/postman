# Wikimedia Enterprise Postman Collection

The Postman collection for the Wikimedia Enterprise APIs, maintained by the Wikimedia Enterprise team. Use it to explore the API, try requests, and check responses before you write code.

[![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)](https://www.postman.com/wikimedia-enterprise)

The public workspace is at [postman.com/wikimedia-enterprise](https://www.postman.com/wikimedia-enterprise). This repository holds the same collection as a file, `Wikimedia Enterprise APIs.postman_collection.json` (Postman collection format v2.1), which you can import directly.

## Quick start

1. **Get the collection.** Fork it from the [public workspace](https://www.postman.com/wikimedia-enterprise), or import the JSON file from this repository (in Postman, click **Import** and choose the file).
2. **Create an account.** [Sign up for a free account](https://dashboard.enterprise.wikimedia.com/signup/) and verify your email.
3. **Store your credentials in the Postman Vault.** Click **Vault** in the footer at the bottom of the Postman window. The first time, Postman asks you to create a vault key, a password that protects the vault on this computer: keep **Save this key to native password manager** ticked so you aren't asked for it again, and keep a copy in your password manager. Then, in your local vault, click **Add new secret** and create two secrets:
    - `wmeUsername`: your Wikimedia Enterprise username, in lowercase
    - `wmePassword`: your Wikimedia Enterprise password

    In **Allowed domains**, enter `https://auth.enterprise.wikimedia.com` for both secrets. That's the only place the collection sends your credentials, and Postman won't use them for any other site.
4. **Let the collection read the vault.** In the vault, click the settings icon at the top right, turn on **Allow Vault secrets in scripts**.
5. **Send a request.** Open **On-demand > Article Lookup**. In the request URL, hover over `{{articlename}}` and type `NASA` in the box that appears. Click **Send**. The first time, Postman asks "Grant Vault access for this execution?": keep **Only this collection** selected and click **Grant Access**. The collection logs in for you and the request returns the article.

You don't need to run **Authentication > Login** yourself or set up an environment. The collection logs in before your first request, keeps your tokens in collection variables, and refreshes the access token before it expires.

**If a request fails:**

- **"Wikimedia Enterprise credentials not found":** check that both secrets exist with exactly those names (step 3) and that **Allow Vault secrets in scripts** is on (step 4).
- **You chose Deny Access by mistake:** in the vault, open **Settings**, then the **Manage access** tab, and click **Grant Access** next to the collection.
- **401 Unauthorized:** check your username and password in the vault. The Postman Console (at the bottom of the window) shows each login and refresh.

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
| **Realtime** | Realtime API: streaming article and Wikidata updates, and Realtime: Batch hourly files. |

Every request links to its entry in the [API reference](https://enterprise.wikimedia.com/docs/api/). The [OpenAPI definition](https://enterprise.wikimedia.com/docs/api/wme-api.yaml) is the full reference for every endpoint and response field.

## Usage notes

- **Account limits** depend on your account. Check your usage in the [Dashboard](https://dashboard.enterprise.wikimedia.com/).
- **Updates:** we update this collection as the API changes. Re-import the file or pull changes into your fork to get new requests.
- **Status:** current API status is at [status.enterprise.wikimedia.com](https://status.enterprise.wikimedia.com/).

## Contributing

Found a problem or have a suggestion? [Open an issue](https://github.com/wikimedia-enterprise/postman/issues). For questions about your account or the APIs, [contact us](https://enterprise.wikimedia.com/contact/).

## License

GPL-3.0. See [LICENSE](LICENSE). Content returned by the APIs comes from Wikipedia and other Wikimedia projects and is licensed under CC BY-SA 4.0.
