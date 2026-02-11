# Git AI 工作流 (Git AI Workflow)

Git 操作往往伴随着大量的重复性文字工作，AI 可以完美代劳。

## 1. 智能 Commit 信息
不要再写 `fix bug` 这种毫无意义的 commit message 了。
- **操作**：
    - `git diff | clip` (复制变更到剪贴板)。
    - **Prompt**:
        ```markdown
        Generate a conventional commit message for these changes.
        Format: <type>(<scope>): <subject>
        ```
    - 或者使用 Cursor/Copilot 自带的 "Generate Commit Message" 按钮（通常是个魔法棒图标）。

## 2. 智能 PR 描述
- **操作**：将整个分支的 Diff 或多次 Commit 内容喂给 AI。
- **Prompt**:
        ```markdown
        Draft a Pull Request description for these changes.
        Include:
        - Summary of changes
        - Impacted areas
        - Testing steps
        ```

## 3. 冲突解决 (Conflict Resolution)
面对复杂的 Merge Conflict，AI 比人眼更准。
- **操作**：在 IDE 中打开冲突文件，选中冲突区域。
- **Prompt**:
    ```markdown
    Resolve this git conflict.
    Current change (HEAD): Added explicit type checking.
    Incoming change: Refactored the variable names.
    Goal: Keep both the type checking and the new names.
    ```

## 4.通过 Git Log 分析历史
- **Prompt**:
    ```markdown
    Analyze the git log of the last 2 weeks.
    Summarize what features were added and what bugs were fixed.
    Identify who contributed the most code (lines of code).
    ```
