#  🔒 secrets-api

A sleek **REST API utility** for managing GitHub Actions Secrets — create, update, delete, and retrieve encrypted secrets securely via code.  

![Made with JavaScript](https://img.shields.io/badge/JavaScript-yellow?logo=javascript&logoColor=black)  
![Powered by Node.js](https://img.shields.io/badge/Node.js-green?logo=node.js&logoColor=white)  
![GitHub REST API](https://img.shields.io/badge/GitHub%20API-black?logo=github&logoColor=white)  

---

##  What It Does

- Securely interacts with GitHub Actions **Secrets API** (create, update, retrieve, delete secrets)  
- Handles encryption via LibSodium (GitHub requires encrypted secrets with a public key) :contentReference[oaicite:0]{index=0}  
- Perfect for automating secret management in CI/CD workflows  

---

##  Technologies & Tools

| Tech / Tool         | Usage                                       |
|---------------------|---------------------------------------------|
| **Node.js**         | Core runtime                                |
| **LibSodium**       | Encryption of secrets before sending to API :contentReference[oaicite:1]{index=1} |
| **GitHub REST API** | Interact with secrets programmatically      |
| **cURL / GitHub CLI** | Optional tools for manual operations       |

---

##  Quickstart Guide

```bash
git clone https://github.com/EternalKnight002/secrets-api.git
cd secrets-api
npm install
````

1. **Get your GitHub Personal Access Token** with `repo` (and `admin:org` if handling org-level secrets). ([vaibhavsagar.com][1], [GitHub Docs][2])
2. **Retrieve repository public key**:

   ```bash
   curl -H "Authorization: Bearer $TOKEN" \
        https://api.github.com/repos/OWNER/REPO/actions/secrets/public-key
   ```
3. **Encrypt your secret** (e.g. using Node.js + LibSodium):

   ````js
   const sodium = require('libsodium-wrappers');
   // Encryption logic here...
   ``` :contentReference[oaicite:3]{index=3}  
   ````
4. **Create or update your secret** using API:

   ````bash
   curl -X PUT -H "Authorization: Bearer $TOKEN" \
        -H "Content-Type: application/json" \
        https://api.github.com/repos/OWNER/REPO/actions/secrets/SECRET_NAME \
        -d '{"encrypted_value":"ENCRYPTED_SECRET","key_id":"PUBLIC_KEY_ID"}'
   ``` :contentReference[oaicite:4]{index=4}
   ````

---

## API Endpoints Overview

* **List secrets** (organization or repo level) — note: values are never exposed ([GitHub Docs][3], [The GitHub Blog][4])
* **Get public key** — necessary to encrypt secrets ([GitHub Docs][5])
* **Create / Update secret** — requires encrypted payload ([Orchestra][6])
* **Get secret metadata** — retrieve details (without secret values) ([Orchestra][7])

---

## Why It Matters

GitHub’s Secrets API is a powerful way to:

* Automate and integrate secret management across projects
* Ensure security via enforced encryption and limited exposure ([The GitHub Blog][4])
* Enable dynamic workflows that respond to changes in credential rotation or environment needs

---

## Project Structure

```
secrets-api/
├── src/              # Main code (API wrappers, encryption logic)
├── examples/         # Sample usage scripts
├── README.md         # You're here!
├── package.json      # Dependencies and scripts
└── .env.example      # Template for environment variables
```

---

## Contribution Guidelines

Contributions, enhancements, or bug reports are **very welcome**! Please:

1. **Fork** this repository
2. Create a new branch: `git checkout -b feature/your-improvement`
3. Commit changes: `git commit -m "Add feature"`
4. Push branch: `git push origin feature/your-improvement`
5. Open a Pull Request — I’ll review and celebrate your contribution!  \:rocket:

---

## License & Credits

Licensed under **MIT** — use, tweak, and build upon it freely.

Built with  by [EternalKnight002](https://github.com/EternalKnight002)
