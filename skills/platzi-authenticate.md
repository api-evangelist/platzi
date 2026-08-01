---
name: Authenticate with JWT
description: Log in to the Platzi Fake Store API, call protected endpoints with a bearer token, and refresh an expired token.
api: openapi/platzi-fake-store-openapi-original.json
operations:
  - AuthController_login
  - AuthController_profile
  - AuthController_refreshToken
---

# Authenticate with JWT

Base URL: `https://api.escuelajs.co/api/v1`.

## Steps
1. **Log in** — `POST /auth/login` with `{ "email": "...", "password": "..." }` (`AuthController_login`). Returns `{ access_token, refresh_token }`. Use a published sandbox user, e.g. `john@mail.com` / `changeme` (see `sandbox/platzi-sandbox.yml`).
2. **Call protected endpoints** — send `Authorization: Bearer <access_token>`. Verify with `GET /auth/profile` (`AuthController_profile`), which returns the current user.
3. **Refresh** — when the access token expires, `POST /auth/refresh-token` with `{ "refreshToken": "<refresh_token>" }` (`AuthController_refreshToken`) to get a new pair.

## Rules
- Bearer JWT only; no OAuth/OIDC scopes — see `authentication/platzi-authentication.yml`.
- Read endpoints (products, categories) need no token; user/CRUD writes benefit from a token.
- A `401 Unauthorized` means the token is missing or expired — refresh and retry.
