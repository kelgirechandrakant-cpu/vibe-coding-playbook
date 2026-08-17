---
name: code-review
description: "Pre-commit code review protocol. Analyzes diffs for antipatterns, logical consistency, API safety, and structural issues. Use when asked to review code, check a diff, or before merging."
---

# Code Review Protocol

When asked to review a piece of code or a Git diff, perform the following strict checks:

## 1. Logic & Correctness
- Does the code actually solve the original problem?
- Are there infinite loops (e.g., missing dependencies in `useEffect`)?
- Is state mutated directly instead of immutably?

## 2. Safety & Security
- Are API keys hardcoded? (They must be in environment variables).
- Is user input rendered directly to the DOM without sanitization (XSS risk)?
- Are API endpoints lacking authentication/authorization checks?

## 3. Maintenance & Cleanliness
- Are there excessive `console.log` statements?
- Is there duplicated logic that should be extracted into a utility function?
- Are the variable names descriptive and accurate?

## 4. Output
Provide a prioritized list of issues. Start with **CRITICAL** (must fix before commit), then **WARNING** (should fix), and end with **NITS** (minor stylistic suggestions).
