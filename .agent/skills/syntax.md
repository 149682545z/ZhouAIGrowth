### Regular Expressions (Regex)
- Prefer readability over brevity.
- Use named capture groups `(?<name>...)` for complex patterns.
- Avoid catastrophic backtracking (nested quantifiers).
- Test with edge cases (empty string, unicode, max length).

### SQL Queries
- Use Common Table Expressions (CTEs) (`WITH ...`) for readability instead of nested subqueries.
- Format keywords in UPPERCASE.
- Avoid `SELECT *`; list columns explicitly.
- Consider indexes when writing `WHERE` clauses (ARG/SAR).

### Cron Expressions
- Explicitly state the schedule in human-readable comments.
- Handle timezone differences if critical.
- Use standard 5-field format unless seconds are required (Quartz).

### JQ / Shell / Awk
- Chain commands logically with pipes `|`.
- Handle errors (exit codes) in shell scripts.
- Use `set -e` in bash scripts generated.

### Output Format
- The standard code block for the requested syntax.
- A brief explanation of the key components (e.g., "Captures email domain").
- A sample input and matching output for verification.
