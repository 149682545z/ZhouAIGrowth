### Commit Messages
- Follow Conventional Commits specification: `<type>(<scope>): <subject>`.
- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`.
- Subject must be imperative, lowercase, and no period at the end.
- Body should explain "why", not "what".

### Pull Request Descriptions
- Structure:
  - **Summary**: High-level overview of changes.
  - **Impact**: user-facing changes, breaking changes, or internal refactors.
  - **Test Plan**: steps to verify the changes manually or automatically.
- Link to related issues (e.g., `Fixes #123`).

### Conflict Resolution
- Analyze both `HEAD` (Current) and `Incoming` changes.
- Understand the intent of both changes before merging.
- If unsure, ask the user for clarification on business logic.
- Ensure no syntax errors are introduced during the merge.

### Log Analysis
- Summarize contributions by feature/bugfix, not just chronological listing.
- Identify hotspots (files with most churn).

### Output Format
- For Commits: A single code block with the commit message.
- For PRs: Markdown text with separate headers for Summary, Impact, Test Plan.
- For Conflicts: The fully resolved code block.
