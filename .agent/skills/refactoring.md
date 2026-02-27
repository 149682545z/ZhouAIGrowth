### Legacy Code Modernization
- Convert Class Components to Functional Components (React/Vue).
- Use `script setup` and Composition API for Vue 3.
- Replace `var` with `let`/`const`.
- Convert CommonJS (`require`) to ES Modules (`import`).
- Preserve all original logic and side effects unless explicitly redundant.

### DRY (Don't Repeat Yourself)
- Identify duplicated logic across files.
- Extract shared logic into `src/utils/` or `src/composables/`.
- Create pure functions where possible to ease testing.
- Update all call sites to use the new abstraction.

### Naming & Readability
- Rename variables to be descriptive (e.g., `isVisible` instead of `flag`).
- Use Guard Clauses (early returns) to flatten deeply nested `if/else` structures.
- Ensure function names start with a verb (e.g., `fetchUser`, `handleClick`).

### Type Augmentation (TS)
- Infer types for untyped JavaScript code.
- Avoid `any`; use specific interfaces or generics.
- Generate `interface` or `type` definitions in strict PascalCase.

### Output Format
- Present the refactored code in a single code block.
- If multiple files are changed, use multiple blocks with `filename` headers.
- Briefly summarize the architectural changes (e.g., "Extracted date logic to `dateUtils.ts`").
