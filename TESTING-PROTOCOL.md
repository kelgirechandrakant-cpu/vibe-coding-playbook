# The Vibe Coder's Test Shield

> **How to use automated test harnesses to physically prevent AI coding agents from breaking your codebase.**

---

## 1. The Core Truth About AI Regressions

AI coding agents are hyper-focused on the prompt directly in front of them. When you say:
> *"Add a dropdown filter to the users list"*

The AI will write code that makes the dropdown filter work. But because it doesn't hold your entire application in memory, it will frequently:
- Accidentally remove a CSS class that broke pagination.
- Alter a type definition that broke the export modal.
- Break a legacy API endpoint that depended on the old function signature.

**Manual testing cannot keep up.** As your project grows past 50 files, testing every screen by hand after every AI prompt takes hours.

**The Solution:** The Automated Test Shield. If an AI knows that tests exist and must pass, it is forced to verify its own diffs before declaring victory.

---

## 2. The 3 Laws of Test-Driven Vibe Coding

### Law 1: Write the Test Before the Feature
Instead of asking the AI to "Build feature X," prompt it:
```text
We are going to build [Feature Name].
Before writing any UI or implementation code:
1. Write a Vitest/Jest unit test in `src/__tests__/feature.test.ts`.
2. Define the expected input, output, and failure cases.
3. Run the test and confirm it fails (Red).
```
Once the test exists, the AI has a tangible finish line. It knows it is done only when `npm test` turns green.

### Law 2: Never Fix a Bug Without a Reproducing Test
When an AI patches a bug without a test, it often introduces the exact same bug 3 weeks later during a refactor.
Prompt:
```text
Do not modify the source code yet.
Write an automated test that reproduces the bug with the exact failing payload.
Confirm the test fails. Then, write the surgical fix until the test passes.
```

### Law 3: The 3-Strike Rule
If an AI tries to fix a bug twice and both attempts fail:
**STOP immediately.**
Do not ask it to try a third time in the same conversation. The model's context is polluted with failed attempts. Step back, write a minimal failing assertion, and start a fresh turn with the test output.

---

## 3. High-Leverage Tests for Vibe Coders

You do not need 100% test coverage. Focus your tests where AI is most prone to breaking things:

| Test Type | What It Protects | Execution Speed |
|---|---|---|
| **Data Ingestion Invariants** | Parsing logic, JSON cleaners, text extractors | $< 50\text{ms}$ |
| **API Boundary Checks** | Request validators, rate limiters, auth middleware | $< 100\text{ms}$ |
| **Export / Output Fidelity** | PDF/PPTX/CSV builders, file serialization | $< 500\text{ms}$ |
| **State Reducers / Bridges** | Cart total calculations, active target context | $< 20\text{ms}$ |

---

## 4. Example: The Anti-Regression Workflow in Practice

```bash
# 1. Ask AI to write the test
"Write a test for the calculateDiscount() utility handling:
 - standard percentage discount
 - 0% discount
 - expired coupon code"

# 2. Run the test (Fails)
npx vitest run src/utils/discount.test.ts

# 3. Ask AI to implement the function
"Implement calculateDiscount() in src/utils/discount.ts until discount.test.ts passes."

# 4. Verify the entire project suite
npm test
```

If all tests pass, make a git commit immediately:
```bash
git commit -m "feat: add calculateDiscount utility with passing unit tests"
```
You now have a permanent safety net. If a future AI prompt breaks discount logic, your test suite will catch it in milliseconds.
