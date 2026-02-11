# 代码辅助工具 (Coding Assistants)

作为开发者，我们要利用好手中的“副驾驶” (Co-pilot)。

## 1. Cursor
Cursor 是目前最强大的 **AI 原生** (AI-Native) 代码编辑器，基于 VS Code 二次开发。
- **核心特色**：
    - **全库索引 (Codebase Indexing)**：Cursor 能够索引整个项目的代码，理解所有的类、函数及其引用关系。
    - **Tab 智能补全**：不仅补全一行，甚至能预测接下来你的多行修改。
    - **Composer (Ctrl+I)**：可以在侧边栏或独立窗口中，用自然语言让它增删改查多个文件。
    - **Chat (Ctrl+L)**：针对当前上下文提问。
- **最佳实践**：
    - 遇到难以理解的遗留代码，选中并按 `Ctrl+L` 问它。
    - 重构时，用 `Ctrl+I` 并在输入框引用相关文件（`@Files`），描述重构目标。
    - 审查代码变更时，使用 Review Mode。

## 2. GitHub Copilot
老牌的 AI 代码补全工具，由微软和 OpenAI 支持。
- **优点**：与 GitHub 生态深度绑定，广泛支持各种 IDE（VS Code, IntelliJ, Visual Studio 等）。
- **主要功能**：
    - 行内自动补全（Ghost Text）。
    - 聊天窗口。
- **适用人群**：习惯使用 IDE 原生插件，追求稳定性和生态集成度的用户。

## 3. Windsurf
新兴的 AI 编辑器，主打对上下文的深度理解和流式体验。
- **特色**：强调“Flow”状态，通过更精准的上下文感知减少思维中断。
- **Cascade**：类似于 Cursor 的 Composer，能够跨文件执行复杂任务。
- **Live Preview**：对前端开发友好。
