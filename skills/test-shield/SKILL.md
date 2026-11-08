---
name: test-shield
description: Directs AI coding agents to write automated regression tests before and alongside feature implementation.
---

# Test-Shield Anti-Regression Skill

Use this skill to direct an AI coding agent to implement features without breaking existing application behavior.

## Core Rules

1. **Test-First Implementation:**
   - When asked to add or modify a core logic function (normalizer, parser, calculator, validator), write the automated unit test in `__tests__/` first.
   - Confirm the test fails against the current state before writing implementation code.

2. **Edge Case Coverage:**
   Every test file must cover at least 3 distinct states:
   - **Happy Path:** Standard expected valid input and output.
   - **Edge Case:** Empty strings, `null`, `undefined`, zero, or extreme values.
   - **Malformed Input:** Corrupted payloads, invalid formatting, or unexpected types.

3. **Execution Verification:**
   - Execute the test runner (e.g. `npx vitest run <path>` or `npm test`).
   - If tests fail, diagnose the failure output without removing test assertions.
   - Never comment out or weaken existing test assertions to make a new test pass.
