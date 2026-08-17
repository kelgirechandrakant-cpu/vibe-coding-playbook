# The Debugging Protocol

The fastest way to destroy a codebase with AI is the "Infinite Debugging Loop." 
This happens when you paste an error into the chat, tell the AI "fix this," and it blindly patches the symptom instead of fixing the root cause.

## Stop Doing This:
> *"This doesn't work. Fix it."*

## Start Doing This (The 9-Step Methodology):
1. **Reproduce the problem:** Can you reliably trigger it?
2. **Capture the exact error:** Get the console log, the network payload, or the terminal crash report.
3. **Identify the affected layer:** Is this a CSS issue? A frontend state issue? A backend database failure?
4. **Inspect relevant code:** Look at the specific file.
5. **Form a hypothesis:** Ask the AI: "Based on this error, what are 2 likely root causes?"
6. **Test the hypothesis:** Add a `console.log` or run a manual test.
7. **Make the smallest appropriate change:** Do not rewrite the whole file.
8. **Test again.**
9. **Check for regressions:** Did fixing this break the feature next to it?

## Examples in Practice

### Example 1: API Timeout (504 Error)
**Bad:** *"I'm getting a 504 on the generation route. Fix it."* (AI adds random timeout flags).
**Good:** *"The `/api/generate` endpoint returns a 504 Gateway Timeout after 30 seconds. This is a Vercel serverless function. We just added a heavy LLM call. Analyze the root cause. Is it a platform limit?"*

### Example 2: Frontend State Bug
**Bad:** *"The cart total is wrong when I delete an item."*
**Good:** *"When calling `removeItem(id)` in `CartContext.tsx`, the item is removed from the array, but the `totalPrice` state does not update. Formulate a hypothesis on why the React state is stale."*

### Example 3: Database Rule Rejection
**Bad:** *"Firebase says missing permissions."*
**Good:** *"Firestore is throwing `FirebaseError: Missing or insufficient permissions` on the `updateDoc` call in `UserProfile.tsx`. Inspect `firestore.rules` for the `users` collection. Are we validating the `request.auth.uid` correctly?"*

**Remember:** If the AI proposes 3 fixes and all 3 fail, **STOP**. You are in a hallucination loop. Step back, look at the logs yourself, and guide the AI.
