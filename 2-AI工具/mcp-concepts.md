# Model Context Protocol (MCP)

AI 模型不再是孤岛。MCP 是连接 AI 与你的数据、工具的通用标准。

## 什么是 MCP？
**Model Context Protocol** 是一个开放标准，它允许开发者构建“服务器 (Server)”，这些服务器可以向 AI 模型（如 Claude, Cursor）提供：
- **上下文 (Context)**：读取文件、数据库、日志。
- **工具 (Tools)**：执行命令、发送请求、操作浏览器。
- **提示词 (Prompts)**：预定义的 Prompt 模板。

## 为什么它很重要？
在没有 MCP 之前，每个 AI 工具（如 Cursor, Windsurf, Claude Desktop）都需要单独对接各种数据源（如 Google Drive, GitHub, Postgres）。
有了 MCP，你只需要写一次 **MCP Server**，所有的 AI 工具都能通用。

## 架构
- **MCP Host**：发起请求的一方（如 Cursor, Claude Desktop）。
- **MCP Server**：提供数据和工具的一方（如 一个连接本地数据库的简单的 Python 脚本）。
- **MCP Client**：协议的实现层。

## 快速开始
在 Cursor 或 Claude Desktop 的设置中，你可以添加 MCP Server。
例如，添加一个 `sqlite` server，你的 AI 就能直接查询本地 SQLite 数据库了。
