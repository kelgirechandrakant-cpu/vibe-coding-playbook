# AGENTS.md — Antigravity & Gemini CLI Guidelines

> Drop this file into `.agents/AGENTS.md` in your project root.

## 1. The Sprint Loop
Every change follows: **Think → Plan → Build → Review → Test → Ship**.
- **Think:** Read the relevant files first. Understand existing patterns.
- **Plan:** State what files you will touch and why before writing code.
- **Build:** One concern per commit. Keep diffs small and reviewable.
- **Review:** Check for type safety, zero layout shifts, and contrast defense.
- **Test:** Run your automated test suite (`npm test`). Never push broken tests.

## 2. Voice & Communication
- **Lead with the point.** Don't bury the answer. State what changed, then explain why.
- **Be concrete.** Name files, line numbers, and exact function names.
- **No AI filler vocabulary.** Do not say "delve", "robust", "comprehensive", "I'd be happy to", or "Great question!".
- **Builder talking to builder.** Short sentences, practical advice.

## 3. Security & Safety
- **No hardcoded secrets.** Secrets remain server-side in `.env`.
- **Sanitize user inputs.** Always use DOMPurify when rendering user HTML.
- **Test before merge.** Run all automated unit and integration tests.
