# 推荐的 MCP Servers

这里列出了一些开箱即用、能显著提升开发效率的 MCP Servers。

## 1. Filesystem (文件系统)
- **功能**：允许 AI 读取和修改本地文件（通常 IDE 自带，但 Claude Desktop 需要单独配置）。
- **用途**：让 AI 分析整个文件夹的项目结构。

## 2. Git
- **功能**：读取 Git 提交历史、Diff、分支信息。
- **用途**：
    - "分析最近 5 次 commit 的变更内容，生成 Release Note。"
    - "查看这个文件的 blame 信息，是谁在什么时候改的？"

## 3. GitHub
- **功能**：搜索代码库、管理 Issue、PR。
- **用途**：
    - "帮我搜索一下 GitHub 上关于 `FastAPI authentication` 的最佳实践。"
    - "创建一个 Issue，描述刚才发现的 Bug。"

## 4. Postgres / SQLite
- **功能**：只读或读写访问数据库。
- **用途**：
    - "查询 `users` 表中最近注册的用户数量。"
    - "检查 `orders` 表的索引是否合理。"
    - **注意**：建议配置只读权限，防止 AI 误删库。

## 5. Brave Search
- **功能**：联网搜索。
- **用途**：让 AI 拥有获取最新实时信息的能力。
    - "查找一下 React 19 的最新 Breaking Changes。"

## 6. Everything (Windows)
- **功能**：利用 Everything 快速搜索本地文件。
- **用途**："帮我找到电脑里所有名为 `secret.key` 的文件。"

---

> 💡 **Tip**: 可以在 [glama.ai/mcp/servers](https://glama.ai/mcp/servers) 找到更多社区贡献的 Server。
