### Test Creation (Red)
- Write tests *before* implementation code.
- Test both happy paths and edge cases (null, negative, boundary values).
- Use descriptive test names ("should calculate discount correctly for VIP").
- Mock external dependencies (Database, API calls) to keep unit tests fast and isolated.

### Implementation (Green)
- Write the *minimum* code required to pass the test.
- Do not over-engineer at this stage.
- Focus on correctness, not performance initially.

### Refactoring (Refactor)
- Improve code structure (extract methods, rename variables) while keeping tests green.
- Optimize performance if benchmarks suggest necessity.
- Ensure no regression.

### Test Frameworks
- JavaScript/TypeScript: Jest, Vitest.
- Python: Pytest, unittest.
- Java: JUnit.

### Output Format
- Provide the Test File content first.
- Provide the Implementation File content second.
- Confirm all tests pass (simulate running them conceptually).
