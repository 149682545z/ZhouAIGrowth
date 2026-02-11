# API 设计 (Schema-First Design)

在写代码之前，先让 AI 帮你写好 API 文档。这能极大降低前后端联调的沟通成本。

## 流程：Schema First

### 1. 描述需求，生成 Schema
- **Prompt**:
    ```markdown
    Design a RESTful API for a "Task Management System".
    Resources: Users, Tasks, Projects.
    Requirements:
    - Tasks belong to a project.
    - Tasks can be assigned to users.
    - Support pagination and filtering.
    Output: OpenAPI 3.0 (YAML) spec.
    ```

### 2. 生成 Mock Server
有了 YAML，直接让 AI 写个简单的 Server 跑起来。
- **Prompt**:
    ```markdown
    Create a lightweight Mock Server using Node.js (express) based on this OpenAPI spec.
    It should return dummy data for all endpoints.
    ```

### 3. 生成前后端代码
- **前端**：根据 Schema 生成 TypeScript 类型定义和 Axios 请求代码。
- **后端**：根据 Schema 生成 Controller 模板和 Pydantic/DTO 模型。

## GraphQL 场景
如果你用 GraphQL，AI 更是如虎添翼。
- **Prompt**:
    ```markdown
    Generate GraphQL Code for my schema.
    Based on these requirements [Requirements], write the `schema.graphql` file.
    Then write the Resolvers in TypeScript.
    ```
