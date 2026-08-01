---
name: Manage catalog (CRUD)
description: Create, update, and delete categories and products in the Platzi Fake Store API sandbox.
api: openapi/platzi-fake-store-openapi-original.json
operations:
  - CategoriesController_create
  - ProductsController_create
  - ProductsController_update
  - ProductsController_delete
  - CategoriesController_delete
---

# Manage catalog (CRUD)

Base URL: `https://api.escuelajs.co/api/v1`. This is a shared public sandbox — writes are non-durable and reset periodically (`sandbox/platzi-sandbox.yml`).

## Steps
1. **Create a category** — `POST /categories` with `{ "name": "...", "image": "https://..." }` (`CategoriesController_create`). Note the returned `id`.
2. **Create a product** — `POST /products` with `{ "title", "price", "description", "categoryId", "images": ["https://..."] }` (`ProductsController_create`). All five fields are required (`CreateProductDto`).
3. **Update a product** — `PUT /products/{id}` with any subset of the product fields (`ProductsController_update`).
4. **Delete** — `DELETE /products/{id}` (`ProductsController_delete`) or `DELETE /categories/{id}` (`CategoriesController_delete`); returns a boolean.

## Rules
- `categoryId` must reference an existing category — create the category first.
- `images` must be a non-empty array of URLs.
- Validation failures return `400` with a `message[]` array — see `errors/platzi-problem-types.yml`.
- No idempotency key is supported; retries create duplicates (`conventions/platzi-conventions.yml`).
