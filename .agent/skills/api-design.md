### RESTful API 设计

- 遵循 HTTP 谓词语义（`GET`、`POST`、`PUT`、`DELETE`、`PATCH`）。
- 对资源使用复数名词（例如 `/users`，而不是 `/user`）。
- 返回标准 HTTP 状态码（2xx、4xx、5xx）。
- 分页：对列表使用 `page`/`limit` 或基于游标的分页。
- 过滤：使用查询参数（例如 `?status=active`）。

### GraphQL Schema 设计

- 对类型使用 PascalCase，对字段使用 camelCase。
- 尽可能避免深度嵌套，以防止性能问题。
- 为 Mutation 定义显式的输入类型（`CreateUserInput`）。
- 默认使用非空字段（`!`），除非是可选的。

### Mock 服务器生成

- 创建一个极简的 Express/Fastify 服务器。
- 返回真实的模拟数据（使用 `faker.js` 等库）。
- 确保启用 CORS 以供前端调用。

### 输出格式

- REST：OpenAPI 3.0 (YAML) 格式。
- GraphQL：SDL (`type User { ... }`)。
- 代码：TypeScript 接口或 Pydantic 模型。
