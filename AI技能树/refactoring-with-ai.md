# AI 重构术 (Refactoring with AI)

重构是偿还技术债务的关键，但往往枯燥且容易出错。AI 是重构的最佳搭档。

## 核心理念：懒人重构 (Lazy Refactoring)
不要自己动手搬运代码，而是指挥 AI 去做。

## 实战场景

### 1. 遗留代码现代化
将老旧的 Class Component 重构为 Functional Component，或者将 jQuery 代码转为 React/Vue。
- **Prompt**:
    ```markdown
    Refactor this Vue 2 Options API component to Vue 3 Composition API using `<script setup>`.
    Keep the logic identical.
    ```

### 2. 提取重复逻辑
当你在多个文件中看到相似的代码块时。
- **Prompt**:
    ```markdown
    I see duplicated logic for date formatting in `A.ts` and `B.ts`.
    Extract it into a new utility function in `src/utils/date.ts`.
    Update both files to use the new utility.
    ```

### 3. 改善可读性
- **Prompt**:
    ```markdown
    Rename variables in this function to be more descriptive based on what they actually do.
    Simplify the nested if-else statements using early returns.
    ```

### 4. 类型增强 (TypeScript)
- **Prompt**:
    ```markdown
    Infer the types for this untyped JavaScript function and add TypeScript interfaces.
    No `any`, please.
    ```
