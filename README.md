# Wikimedia Enterprise Postman Collection

The Postman collection for the Wikimedia Enterprise APIs, maintained by the Wikimedia Enterprise team. Use it to explore the API, try requests, and check responses before you write code.

[![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)](https://www.postman.com/wikimedia-enterprise)

The public workspace is at [postman.com/wikimedia-enterprise](https://www.postman.com/wikimedia-enterprise). This repository holds the same collection as a file, `wikimedia-enterprise-apis.postman_collection.json` (Postman collection format v2.1), which you can import directly.

## Quick start

1. **Get the collection.** Fork it from the [public workspace](https://www.postman.com/wikimedia-enterprise), or import the JSON file from this repository (in Postman, click **Import** and choose the file).
2. **Create an account.** [Sign up for a free account](https://dashboard.enterprise.wikimedia.com/signup/) and verify your email.
3. **Store your credentials in Postman Vault.** Your local vault keeps them encrypted and doesn't sync them to the Postman Cloud. Click **Vault** in the footer of the Postman window. If Postman asks you to create a vault key, keep a copy in your password manager. Then click **Add new secret** and create two secrets:
    - `wmeUsername`: your Wikimedia Enterprise username, in lowercase
    - `wmePassword`: your Wikimedia Enterprise password

    In **Allowed domains**, enter `https://auth.enterprise.wikimedia.com` for both.
4. **Let the collection read the vault.** In the vault, click **Settings** and turn on **Allow Vault secrets in scripts**.
5. **Send your first request.** Open **Metadata > Projects Available** and click **Send**. When Postman asks "Grant Vault access for this execution?", keep **Only this collection** selected and click **Grant Access**.

That's all the setup. The collection logs in before your requests and refreshes your access token when it needs to, so you don't need to run **Authentication > Login** or set up an environment.

**If a request fails:**

- **"Wikimedia Enterprise credentials not found":** check that both secrets exist with exactly those names (step 3) and that **Allow Vault secrets in scripts** is on (step 4).
- **You chose Deny Access by mistake:** in the vault, open **Settings**, then the **Manage access** tab, and click **Grant Access** next to the collection.
- **401 Unauthorized:** check your username and password in the vault. The Postman Console shows each login and refresh.

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
| **Authentication** | Login, token refresh and revoke, password changes, and the forgot-password flow. |
| **Metadata** | Available projects, languages, namespaces, and project codes. |
| **Snapshot API** | List, inspect, and download project snapshots and their chunks. The **Structured Contents Snapshots (Beta)** and **Wikidata Snapshots (Beta)** folders do the same for Structured Contents and for Wikidata items and properties. |
| **On-demand API** | Look up the current version of an article and its Structured Contents (Beta). The **Wikidata (Beta)** folder looks up Wikidata items, properties, and labels. |
| **Realtime API** | Stream article and Wikidata updates. The **Realtime: Batch** folder lists and downloads the hourly batch files, for projects and for Wikidata (Beta). |

The collection covers every endpoint in version 2.0.0 of the API. Where an endpoint also accepts `GET`, the `POST` request's description says so. Every request links to its entry in the [API reference](https://enterprise.wikimedia.com/docs/api/). The [OpenAPI definition](https://enterprise.wikimedia.com/docs/api/wme-api.yaml) is the full reference for every endpoint and response field.

## Usage notes

- **Downloads:** download requests return a `307` redirect to a presigned URL that is valid for 60 seconds. The collection doesn't follow it, because snapshot files can be over 100 GB. Copy the URL from the `Location` header (the response body shows it as a link too) and download it with a tool like `curl --location`. The matching **... Headers** request shows the file size first.
- **Account limits** depend on your account. Check your usage in the [Dashboard](https://dashboard.enterprise.wikimedia.com/).
- **Updates:** we update this collection as the API changes. Re-import the file or pull changes into your fork to get new requests.
- **Status:** current API status is at [status.enterprise.wikimedia.com](https://status.enterprise.wikimedia.com/).

## Contributing

Found a problem or have a suggestion? [Open an issue](https://github.com/wikimedia-enterprise/postman/issues). For questions about your account or the APIs, [contact us](https://enterprise.wikimedia.com/contact/).

## License

GPL-3.0. See [LICENSE](LICENSE). Content returned by the APIs comes from Wikipedia and other Wikimedia projects and is licensed under CC BY-SA 4.0.
