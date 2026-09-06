# Exploring and Testing APIs with Postman - GitHub Gists API

This repository contains my submission for the "Exploring and Testing APIs with Postman" assignment. I tested the **GitHub REST API**, specifically the **Gists** resource, demonstrating authentication, CRUD operations, error handling, and automated testing via Postman's Collection Runner.

## Repository Contents

| File | Description |
|---|---|
| `API_Testing_Report.pdf` | Full written report covering API choice, authentication, CRUD operations, environment/variables, automation, and error handling |
| `API_assignment.postman_collection.json` | Exported Postman Collection containing all requests, scripts, and configuration |
| `API_Testing_env.postman_environment.json` | Exported Postman Environment containing variable definitions (token value excluded/reset before export) |
| `README.md` | This file |

## API Overview

- **Base URL:** `https://api.github.com`
- **Resource tested:** Gists (`/gists`)
- **Authentication:** Personal Access Token (PAT), sent as a Bearer token

## Authentication Setup

1. A GitHub Personal Access Token (classic) was generated via **GitHub → Settings → Developer settings → Personal access tokens**, scoped to the `gist` permission.
2. The token is stored as the `auth_token` variable in the Postman environment.
3. Bearer Token authentication is configured once at the **collection level**, using `{{auth_token}}`.
4. Individual requests inherit this via **"Inherit auth from parent"**.

## Environment Variables

| Variable | Purpose |
|---|---|
| `base_url` | API root: `https://api.github.com` |
| `auth_token` | Personal Access Token used for Bearer authentication |
| `gist_id` | ID of the most recently created gist; set automatically by the Create request's test script |

## Requests Included

| Request | Method | Endpoint | Purpose |
|---|---|---|---|
| Create Gist | POST | `/gists` | Creates a new gist |
| Get Gist | GET | `/gists/{gist_id}` | Retrieves the created gist |
| Update Gist | PATCH | `/gists/{gist_id}` | which updates the gist's description/content |
| Delete Gist | DELETE | `/gists/{gist_id}` | Deletes the gist |


Each request includes a Postman test script verifying the expected status code (and relevant response data where applicable).

## Running the Collection

1. Import `API_assignment.postman_collection.json` and `API_Testing_env.postman_environment.json` into Postman.
2. Select the imported environment from the top-right dropdown.
3. Open the environment and set your own `github_token` value (not included in the export for security).
4. Run requests individually, or use **Collection Runner** (three-dot menu on the collection → Run Collection) to execute the full sequence automatically:
   ```
   Create → Get → Update → Delete 
   ```
   This order matters: Get, Update, and Delete all depend on the `gist_id` set by the Create request.

## Notes

- GitHub does not provide a login/token-refresh endpoint for Personal Access Tokens (tokens are generated manually on GitHub's website), so the assignment's automatic token-refresh pattern was adapted to a pre-request script that verifies the token variable is present before a request runs.
- Full explanations, screenshots, and reflection are available in `API_Testing_Report.docx`.

## AUTHOR

*Elvire AKAYEZU*