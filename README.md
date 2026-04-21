# Wikimedia Enterprise Postman Collection 🐿️

Welcome to the official Postman collection for **Wikimedia Enterprise**. This repository provides a comprehensive set of API requests to help you explore, test, and integrate Wikipedia's high-volume data services.

[![Postman](https://img.shields.io/badge/Postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white)](http://postman.com/wikimedia-enterprise)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge)](https://opensource.org/licenses/Apache-2.0)

##  Official Workspace 🚀
Interact with the collection live at **[http://postman.com/wikimedia-enterprise](http://postman.com/wikimedia-enterprise)**

---

##  Quick Start 🐿️

1.  **Visit the Workspace**: Click the link above to view the public Wikimedia Enterprise workspace.
2.  **Fork the Collection**: Fork the collection to your own Postman workspace to start making requests.
3.  **Configure Auth**: 
    * [Sign up for an account](https://dashboard.enterprise.wikimedia.com/signup/).
    * Add your Enterprise username and password to your local vault in the variables `{{vault:wmeUsername}}` and `{{vault:wmePassword}}`.
    * Use the [Login endpoint](https://www.postman.com/wikimedia-enterprise/workspace/57f4bfe2-972e-471d-8b4b-4e8a8bb6db77/request/47290592-18e31479-944d-4adc-9466-c47a910394ae?action=share&source=copy-link&creator=47290592) (Authentication -> Login ), which will automatically populate the environment variables `{{access_token}}` and `{{refresh_token}}`.
4. **Make your first call**: [get the NASA Wikipedia page in the On-demand API](https://www.postman.com/wikimedia-enterprise/workspace/57f4bfe2-972e-471d-8b4b-4e8a8bb6db77/example/47290592-fc19dec5-0d30-4e51-858c-504b7d95702a?action=share&source=copy-link&creator=47290592).


##  What's Inside? 📦

| Feature | Description |
| :--- | :--- |
| **Snapshot API** | Access bulk data dumps for large-scale analysis. |
| **On-demand API** | Query specific articles or metadata with low latency. |
| **Realtime API** | Stream Wikimedia project changes as they happen. 
| **Structured Data** | Deep integration with Wikidata and Commons. |

## Usage Notes 🛠️
* **Environment Variables**: We recommend using Postman Environments to manage your access tokens securely.
* **Account limits**: Ensure you are aware of the usage limits associated with your free or paid account.
* **Updates**: This collection is updated regularly. Be sure to pull changes or re-fork if you notice new endpoints in the documentation.

## Contributing 🤝
Found a bug or have a suggestion? 
1.  Open an [Issue](https://github.com/wikimedia-enterprise/postman/issues).
2.  Submit a Pull Request.
3.  Reach out via the [Wikimedia Enterprise help center](https://enterprise.wikimedia.com/contact/).

---
*Maintained with 🐿️ by the Commercial Partnerships Division of the Wikimedia Foundation.*
