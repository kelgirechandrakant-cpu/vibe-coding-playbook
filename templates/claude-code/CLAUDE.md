# CLAUDE.md — Instructions for Claude Code CLI

> Drop this file into your project root when using Claude Code CLI.

## Project Guidelines

### Build & Test Commands
- **Install:** `npm install`
- **Dev Server:** `npm run dev`
- **Lint / Typecheck:** `npm run lint` or `npx tsc --noEmit`
- **Run Tests:** `npm test` or `npx vitest run`

### Core Development Principles
1. **Understand Before Modifying:**
   - Always run `glob` or `grep` before creating files to ensure you are not duplicating existing utilities.
   - Inspect imports and caller references before altering function signatures.
2. **Smallest Viable Diff:**
   - Make surgical edits. Do not reformat unrelated code in the same change.
   - Keep changes scoped to 1–3 files per turn.
3. **No Unverified Claims:**
   - Only state tests passed if you ran the command and verified zero exit errors.
   - If you cannot run tests, state your mental execution walk-through explicitly.
4. **Security & Secrets:**
   - Never embed API keys in client code or commit `.env` files.
   - Check `.gitignore` before creating temporary files or bundles.
