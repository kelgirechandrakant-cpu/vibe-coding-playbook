# Vibe Coding Playbook

> **How to use AI to build real software without turning your codebase into a mess.**

A playbook for developers, students, and engineers who want to build production-grade applications using AI coding agents (like Cursor, Lovable, Antigravity, or Copilot) **without losing control of their architecture.**

## 🛑 The Status Quo We Are Fixing
The most common vibe-coding failure loop looks like this:
1. Ask AI to build the entire app.
2. AI generates thousands of lines of spaghetti code.
3. You ask for a new feature.
4. Something breaks.
5. You tell the AI "Fix this error."
6. The AI changes 8 files and creates 3 new bugs.
7. **Infinite debugging loop.**

This repository is designed to cure that exact problem.

## 🧠 The 10 Principles of Vibe Coding

1. **AI is the implementation engine, not the owner of the architecture.**
2. **Never blindly trust generated code.**
3. **Build in small, testable increments.**
4. **Understand the error before changing the code.**
5. **Prefer root-cause fixes over patches.**
6. **Keep the developer in control of the codebase.**
7. **A prototype is not a production application.**
8. **Every AI-generated change should be verifiable.**
9. **Context is part of the prompt.**
10. **The goal isn't to write less code. The goal is to build better software with AI.**

## 📂 Repository Structure

- `VIBECODING.md`: The core playbook and methodology for planning, coding, and debugging.
- `AGENTS.md`: The master ruleset. Copy-paste this into your project to tame your AI agent.
- `PROMPTS.md`: Highly structured workflow prompts (not generic "build me a SaaS" prompts).
- `DEBUGGING.md`: The framework for escaping the infinite debugging loop.
- `PRODUCTION-CHECKLIST.md`: How to take an AI prototype to a real production release.
- `skills/`: Modular "AI Personas" you can copy into your project for code review, security audits, and more.

## 🚀 How to Use This Repo

1. Read **`VIBECODING.md`** to understand the workflow.
2. Copy **`AGENTS.md`** into your project's `.agents` or `.cursorrules` folder.
3. Copy the **`skills/`** folder into your project to give your AI specialized auditing capabilities.
4. Keep **`DEBUGGING.md`** open when your AI inevitably breaks something.

---
*Built with insights from the development of [Student Suite (PPT Maker)](https://pptmaker.co.in).*
