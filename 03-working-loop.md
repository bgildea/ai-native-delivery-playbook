# 3. The working loop

## 1. Plan before code

Ask for a plan first: which files change, in what order, and how it will be tested. Read it. Most expensive mistakes are visible in the plan and cheap to fix there. Claude Code's plan mode exists for exactly this.

## 2. One small change at a time

Ask for the smallest change that moves a test from red to green. Commit it. Repeat. Small commits are easy to review, easy to revert, and keep the model working against a stable base.

## 3. Tests first, or at least tests alongside

- Turn acceptance criteria into failing tests
- Let the model implement until they pass
- Read the tests as carefully as the code. A model can write a test that passes for the wrong reason

## 4. Run everything locally

Lint, type checks, unit tests, then try the feature by hand. "It compiles" is not done.

## 5. Stop when it loops

If two attempts at the same fix fail, stop and re-think. Re-state the problem, add an example, or narrow the task. A third identical prompt rarely works.

## Anti-patterns

| Anti-pattern | Instead |
| --- | --- |
| "Build the whole feature" in one prompt | A plan, then small steps |
| Accepting a large diff because the tests pass | Read it; if you can't, split it |
| Fixing model mistakes by hand without telling it | Say what was wrong so the next step builds on the fix |
| Copying production data into a prompt to debug | Use fixtures or redacted samples |
