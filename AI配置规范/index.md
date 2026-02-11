# AI 配置规范 (AI Configuration Standards)

为了保证团队成员使用 AI 辅助编码时的一致性和高质量，我们需要统一 AI 的“人设”和行为准则。

## 核心配置：`.cursorrules`

`.cursorrules` 是 Cursor 编辑器的项目级配置文件。通过它，我们可以定义 AI 在该项目中的行为模式、代码风格和最佳实践。

### 为什么需要它？
- **统一风格**：强制 AI 生成符合团队规范的代码（如命名约定、目录结构）。
- **减少废话**：禁止 AI 解释显而易见的代码，直接给结果。
- **避免坑**：告诉 AI 哪些库不要用，哪些模式已废弃。

### 推荐模板
在项目根目录创建 `.cursorrules` 文件，内容如下：

```markdown
# Role
You are a Senior Full-Stack Engineer expert in [Tech Stack, e.g., Vue 3, TypeScript, Python 3.10].

# Coding Standards
- **Naming**: Use camelCase for variables/functions, PascalCase for classes/components.
- **Typing**: strict boolean in tsconfig is on. No `any`. Explicit return types.
- **Comments**: Write JSDoc for exported functions.
- **Structure**:
  - Components go to `src/components`.
  - Utils go to `src/utils`.

# Behaviors
- **Conciseness**: Don't explain basic concepts. Just show the code.
- **Refactoring**: When modifying code, always prefer immutable patterns.
- **Testing**: Always suggest unit tests (Vitest) for new utility functions.

# Forbidden
- Do not use `var`.
- Do not use `moment.js` (use `dayjs` instead).
```

## 其他工具配置
- **VS Code Settings**: 统一 `editor.formatOnSave` 等设置。
- **Git Hooks**: 使用 Husky 在 commit 前运行 Lint 检查，确保 AI 生成的代码符合规范。
