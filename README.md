# Vibe Coding Playbook

> **A practical guide to using AI coding agents to build, debug, secure, and ship real software without losing control of the codebase.**

---

## The Problem

We've all been there. You have a great idea and spin up an AI coding agent:

```text
Idea
↓
Ask AI to build everything
↓
Looks impressive
↓
Add more features
↓
Architecture starts drifting
↓
Something breaks
↓
AI patches it
↓
Another thing breaks
↓
Infinite debugging loop
↓
Unmaintainable codebase
```

This repository teaches a better workflow. **Vibe coding isn't about letting AI build everything for you. It's about learning how to direct, constrain, inspect, test, and improve AI-generated software.**

## Who Is This For?
**Primary Audience:** Students, junior developers, and self-taught developers building their first serious SaaS or web application. If you understand basic programming but struggle with architecture, debugging, or production-readiness, this playbook is for you.

**Who it's NOT for:** This is not a repository of "Make me a SaaS" prompts for non-technical founders, nor is it a comprehensive architecture manual for senior engineers.

## The Core Principles

1. **AI is the implementation engine, not the owner of the architecture.**
2. **The developer owns the final result.**
3. **Never blindly trust generated code.**
4. **Build in small, verifiable increments.**
5. **Understand the problem before asking AI to modify code.**
6. **Prefer root-cause fixes over patches.**
7. **Context is part of the prompt.**
8. **Every significant AI-generated change should be verified.**
9. **A working prototype is not automatically production-ready software.**
10. **The goal is not to write less code. The goal is to build better software with AI.**

## Recommended Workflow
**Plan → Context → Implement → Inspect → Test → Verify → Commit**

For debugging:
**Reproduce → Diagnose → Isolate → Fix → Test → Verify**

## Repository Structure

- [**`VIBECODING.md`**](./VIBECODING.md) - The core conceptual playbook and methodology.
- [**`AGENTS.md`**](./AGENTS.md) - Instructions to copy into your project to align your AI agent.
- [**`PROMPTS.md`**](./PROMPTS.md) - A prompt library organized by development phase (Planning, Implementation, Review).
- [**`DEBUGGING.md`**](./DEBUGGING.md) - The guide to escaping the infinite debugging loop.
- [**`PRODUCTION-CHECKLIST.md`**](./PRODUCTION-CHECKLIST.md) - How to take your local prototype to the real world.
- [**`skills/`**](./skills/) - Reusable instructions and personas that AI coding agents can follow.
- [**`examples/`**](./examples/) - Good vs. bad workflows and prompts.
- [**`case-studies/`**](./case-studies/) - Real-world examples of this methodology in practice (e.g., PPT Maker).

## Quick Start

1. Read [`VIBECODING.md`](./VIBECODING.md) to understand the fundamental shift in how you should interact with AI.
2. Copy [`AGENTS.md`](./AGENTS.md) into your project's `.agents` or `.cursorrules` folder.
3. Keep [`DEBUGGING.md`](./DEBUGGING.md) open when you hit your first major error.

## Contribution & License
Read our [Contribution Guidelines](./CONTRIBUTING.md) to submit new skills, debugging patterns, or case studies.

Licensed under the [MIT License](./LICENSE).
