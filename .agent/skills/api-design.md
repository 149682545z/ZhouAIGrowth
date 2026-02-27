### RESTful API Design
- Adhere to HTTP verbs semantics (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`).
- Use plural nouns for resources (e.g., `/users`, not `/user`).
- Return standard HTTP status codes (2xx, 4xx, 5xx).
- Pagination: Use `page`/`limit` or cursor-based pagination for lists.
- Filtering: Use query parameters (e.g., `?status=active`).

### GraphQL Schema Design
- Use PascalCase for Types and camelCase for fields.
- Avoid deep nesting if possible to prevent performance issues.
- Define explicit input types for mutations (`CreateUserInput`).
- Use non-nullable fields (`!`) by default unless optional.

### Mock Server Generation
- Create a minimal Express/Fastify server.
- Return realistic dummy data (use libraries like `faker.js`).
- Ensure CORS is enabled for frontend consumption.

### Output Format
- For REST: OpenAPI 3.0 (YAML) format.
- For GraphQL: SDL (`type User { ... }`).
- For Code: TypeScript Interfaces or Pydantic Models.
