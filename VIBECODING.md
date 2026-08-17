# Vibe Coding Playbook

This document is the primary conceptual playbook for building software with AI.

## 1. What Vibe Coding Actually Is
Vibe coding is the process of using AI agents to accelerate software implementation. However, it is not "tell the AI to build my app." It is an engineering partnership where **you own the architecture and decisions**, and the AI handles the typing and implementation details.

## 2. The Difference Between Prototype and Production
An AI can build a working prototype on `localhost` in 10 minutes. A prototype proves an idea works. Production software handles bad network connections, malicious user input, database scaling, and edge cases. Do not confuse the two.

## 3. Before You Start Coding
Never write code (or ask AI to write code) on day one. You must define the user flow, the data model, and the technical constraints. The AI can help you brainstorm these, but you must lock them in before writing the first component.

## 4. Understanding the Existing Codebase
AI agents have limited context windows. If your project has 50 files, the AI might only be looking at 3 of them. You must understand how your codebase is wired together so you can point the AI at the right files.

## 5. Planning With AI
Use the AI as a sounding board. Ask it: "If we build the feature this way, what are the three most likely ways it will break?" Let the AI spot the architectural flaws before you start coding.

## 6. Giving AI the Right Context
Context is everything. When asking an AI to build a new route, provide the database schema, the authentication middleware, and the exact files it needs to modify. Do not rely on it to "guess" your folder structure.

## 7. Breaking Work Into Small Tasks
"Build a dashboard" is a terrible prompt. "Create the layout grid for the dashboard," followed by "Build the user statistics card," followed by "Fetch the data from the API" is how you successfully vibe code. See a concrete example in [feature implementation](./examples/feature-implementation.md).

## 8. Implementing Features
Follow the **Plan → Context → Implement** loop. Ensure the AI is only modifying what it needs to modify.

## 9. Reviewing AI-Generated Code
Never blindly accept a diff. Read the code. Did it import a massive 2MB library just to parse a date? Did it remove your error boundary? **The developer owns the final result.** Use the [code review skill](./skills/code-review/SKILL.md) to automate this.

## 10. Testing AI-Generated Changes
Run the code locally. Click the buttons. Disconnect your wifi and see what happens. The AI will often claim "I fixed the issue," but it only fixed it in its own imagination.

## 11. Debugging
See [`DEBUGGING.md`](./DEBUGGING.md) for the full protocol. Never tell the AI "fix this." Tell it the symptoms, formulate a hypothesis, and isolate the layer.

## 12. Refactoring
When a file gets messy, use the AI to break it apart. But never mix feature development with refactoring. Refactor first, verify it works exactly as before, then add the new feature.

## 13. Security
AI optimizes for making things work, which often means bypassing security. It will happily put API keys in the browser bundle or leave Firestore rules wide open. See [`PRODUCTION-CHECKLIST.md`](./PRODUCTION-CHECKLIST.md) and use the [security audit skill](./skills/security-audit/SKILL.md).

## 14. Performance
Watch for excessive `useEffect` dependencies, lack of pagination, and unoptimized images. Ask the AI: "Is there a more performant way to write this specific function?"

## 15. SEO
AI will often build Single Page Applications (SPAs) that search engines struggle to crawl. You must explicitly direct it to add metadata, semantic HTML, and correct routing.

## 16. Deployment
Never let an AI auto-deploy to production without a human reviewing the `git diff`. Ensure environment variables are set up securely in your hosting provider.

## 17. Maintaining the Project
Keep your `AGENTS.md` updated as your project evolves. If you change your naming conventions, tell the AI so it doesn't revert to old habits.

## 18. When NOT to Let AI Make the Decision
Do not let the AI choose your database, your authentication provider, or your core framework without you doing independent research. The AI will often recommend what is most popular in its training data, not what is right for your specific constraints. See the [PPT Maker case study](./case-studies/pptmaker.md) for a concrete example of ceding too much architectural control.
