# 语法生成 (Syntax Generation)

有些语法（如 Regex, SQL, Cron）是“写了一次就忘”，或者“每次都要查文档”。把这些脑力负担交给 AI。

## 1. 正则表达式 (Regex)
Regex 是典型的“天书”。
- **Prompt**:
    ```markdown
    Write a Regex to match a valid email address.
    Rules:
    - Must allow standard domains (com, net, org).
    - Must NOT allow plus signs (+) in the local part.
    - Case insensitive.
    And explain how it works step-by-step.
    ```
- **验证**：让 AI 生成几个测试用例（匹配的和不匹配的）来验证它写的 Regex。

## 2. SQL 查询
尤其是复杂的 JOIN 和 窗口函数。
- **Prompt**:
    ```markdown
    Table User: id, name, created_at
    Table Order: id, user_id, amount, created_at

    Write a SQL query (PostgreSQL) to find the top 10 users by total spending in the last month.
    Include their rank and total amount.
    Use Window Functions if necessary.
    ```

## 3. Cron 表达式
- **Prompt**:
    ```markdown
    Write a Cron expression that runs "Every Tuesday at 3:00 AM, but only in January and February".
    ```

## 4. JQ (JSON Query)
处理 JSON 数据的利器，但语法也很晦涩。
- **Prompt**:
    ```markdown
    I have a huge JSON log file.
    Write a `jq` command to extract the `timestamp` and `error_message` fields where `level` is "ERROR".
    ```
