---
name: Browse and filter products
description: List, paginate, filter, and look up products (and their categories) in the Platzi Fake Store API. No authentication required.
api: openapi/platzi-fake-store-openapi-original.json
operations:
  - ProductsController_getAll
  - ProductsController_getProduct
  - ProductsController_getProductBySlug
  - ProductsController_getRelatedProducts
  - CategoriesController_getAll
  - CategoriesController_getProductsByCategory
---

# Browse and filter products

Base URL: `https://api.escuelajs.co/api/v1`. Read endpoints are fully open — no token needed.

## Steps
1. **List with pagination** — `GET /products?limit=10&offset=0` (`ProductsController_getAll`). Increase `offset` by `limit` to page.
2. **Filter** — combine query params: `title`, `price`, `price_min` & `price_max`, `categoryId`, `categorySlug`. Example: `GET /products?price_min=50&price_max=100&categoryId=1`.
3. **Fetch one** — by id `GET /products/{id}` (`ProductsController_getProduct`) or by slug `GET /products/slug/{slug}` (`ProductsController_getProductBySlug`).
4. **Related products** — `GET /products/{id}/related` (`ProductsController_getRelatedProducts`).
5. **Browse categories** — `GET /categories` (`CategoriesController_getAll`), then `GET /categories/{id}/products` (`CategoriesController_getProductsByCategory`).

## Conventions
- Pagination is offset-based (`limit`/`offset`) — see `conventions/platzi-conventions.yml`.
- Each product embeds its full `category` object and an `images[]` array.
- Errors follow `{message, error, statusCode}` — see `errors/platzi-problem-types.yml`.
