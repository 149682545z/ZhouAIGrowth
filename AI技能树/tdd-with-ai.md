# AI 驱动的测试驱动开发 (AI-First TDD)

TDD (Test-Driven Development) 很好，但写测试代码很累。让 AI 来帮你写测试，你只负责写实现（或者连实现也让 AI 写）。

## 流程：Red - Green - Refactor (AI Edition)

### Step 1: 描述需求，生成测试 (Red)
不要先写业务代码，先告诉 AI 你想要什么，让它写出“注定因找不到实现而失败”的测试用例。
- **Prompt**:
    ```markdown
    Create a unit test (using Jest/Vitest) for a function `calculateDiscount(price, userType)`.
    Rules:
    - VIP users get 20% off.
    - Regular users get no discount.
    - Price cannot be negative.
    ```

### Step 2: 生成实现 (Green)
运行测试，报错。然后让 AI 实现代码以通过测试。
- **Prompt**:
    ```markdown
    Implement the `calculateDiscount` function to pass the above tests.
    ```

### Step 3: 重构 (Refactor)
代码跑通了，但可能很丑。让 AI 优化。
- **Prompt**:
    ```markdown
    The implementation is working, but the `if-else` chain is too long. Refactor it using a strategy pattern or lookup table.
    ```

## 优势
- **覆盖率高**：AI 擅长枚举边界情况（空值、负数、极大值）。
- **思维清晰**：先定接口（测试），再定实现，符合高内聚低耦合的设计原则。
