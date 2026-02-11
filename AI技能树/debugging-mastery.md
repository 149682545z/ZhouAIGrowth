# 深度调试 (Deep Debugging with AI)

调试不仅仅是修 Bug，更是理解系统的过程。

## 技巧 1：解释报错堆栈
不要只看最后一行报错。把整个 Stack Trace 扔给 AI。
- **Prompt**:
    ```markdown
    Analyze this stack trace. It seems the crash happens in `DataProcessor.py`, but I suspect the root cause is upstream data.
    Trace: [PASTE TRACE HERE]
    ```

## 技巧 2：像鸭子一样思考 (Rubber Duck Debugging)
当你毫无头绪时，把 AI 当作你的“橡皮鸭”，向它解释你的代码逻辑。通常在解释的过程中，你自己就发现了问题，或者 AI 会指出逻辑漏洞。
- **Prompt**:
    ```markdown
    I'm trying to implement a cache mechanism here.
    My logic is:
    1. Check Redis.
    2. If miss, query DB.
    3. Update Redis.
    But sometimes I get stale data. Can you check my concurrency logic? Here is the code.
    ```

## 技巧 3：生成调试代码
让 AI 帮你写临时的 Logging 代码，或者专门的调试脚本。
- **Prompt**:
    ```markdown
    I can't reproduce this race condition locally.
    Write a script that spawns 100 concurrent requests to this endpoint to stress test the locking mechanism.
    ```

## 技巧 4：假设性分析
- **Prompt**:
    ```markdown
    What would happen if the network latency between Service A and Service B increases to 5s?
    Review this timeout handling code and predict potential failures.
    ```
