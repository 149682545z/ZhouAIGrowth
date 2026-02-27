### Stack Trace Analysis
- Inspect the entire stack trace, not just the last line.
- Identify user code vs library code.
- Check for common errors (NullReference, index out of bounds, timeout).

### Logging Strategy
- Suggest adding `console.log`/`print` statements at key checkpoints if reproduction is hard.
- Log inputs, outputs, and critical state variables.
- Use structured logging (JSON) if possible.

### Root Cause Analysis (RCA)
- Formulate a hypothesis based on observed behavior.
- Validate hypothesis with reasoning or proposed test.
- Check for recent changes (git blame) that might have introduced the bug.
- Consider environment differences (Dev vs Prod, Windows vs Linux).

### Rubber Ducking
- Explain the code logic step-by-step to the user to uncover logical flaws.
- Verify assumptions about external systems (API availability, Database state).

### Output Format
- Summary of the likely cause.
- Proposed fix (code block).
- Verification steps (how to confirm it's fixed).
