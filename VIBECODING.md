# Vibe Coding Playbook

This document outlines the core methodology for successfully partnering with an AI coding agent. The goal is to move from "Prompt & Pray" to "Plan, Implement, Verify."

## 1. Before Coding: Define the System

The biggest mistake vibe coders make is telling the AI to "Build a SaaS." Before generating a single line of code, you must define the following (either yourself or by brainstorming *with* the AI):

*   **Requirements & User Flow:** What exactly should happen when a user clicks the main button?
*   **Architecture:** Are we using a monolithic Next.js app, or React + Express?
*   **Data Model:** What does the database schema look like?
*   **Constraints:** e.g., "Do not use paid APIs. Keep the bundle size small."

*Action:* Use the **Project Planning Prompt** in `PROMPTS.md` to lock this down before you start coding.

## 2. During Coding: The Incremental Loop

Do not give the AI scope over the entire application. Work in small, verifiable units.

**The Golden Loop:**
1.  **Prompt:** "Build the authentication UI component."
2.  **Implement:** AI generates the code.
3.  **Inspect:** Read the diff. Did it import heavy libraries? Did it break existing CSS?
4.  **Test:** Run it in the browser.
5.  **Verify:** Does it meet the requirement?
6.  **Commit:** `git commit -m "feat: add auth UI"`

Never move to step 2 (e.g., "Now build the dashboard") until you have successfully committed step 1.

## 3. When Something Breaks: Stop the Patching

When an AI writes code that throws an error, the instinct is to paste the error back into the chat and say "Fix this." **Do not do this.**

This leads to the **Infinite Debugging Loop**:
1. AI patches symptom A.
2. Patch breaks symptom B.
3. AI patches symptom B.
4. Patch breaks symptom A.
5. Codebase becomes spaghetti.

*Action:* See `DEBUGGING.md` for the correct protocol. You must identify the *root cause* before allowing the AI to change the code.

## 4. Before Deployment: The Reality Check

A web app that works on your `localhost:3000` is usually a prototype, not a production application. AI agents often skip crucial production steps because they optimize for getting the immediate task working.

You must explicitly audit for:
*   API Security & Rate Limiting
*   Environment Variable protection
*   Mobile Responsiveness
*   Error boundaries and fallback UI

*Action:* Run through `PRODUCTION-CHECKLIST.md` before sharing your link with real users.
