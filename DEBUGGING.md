# The Debugging Protocol

The fastest way to destroy a codebase with AI is the "Infinite Debugging Loop." 
This happens when you paste an error into the chat, tell the AI "fix this," and it blindly patches the symptom instead of fixing the root cause.

## The Rule of 3 Failures
If the AI tries to fix an error 3 times and fails, **STOP**. 
You are going down a rabbit hole. The AI is hallucinating fixes based on faulty assumptions. You must manually intervene, read the logs, and guide the AI back to reality.

## Bad vs. Good Debugging Prompts

### ❌ The Bad Prompt (Symptom Patching)
> "I'm getting a 504 error on the dashboard. Fix it."
*Result:* The AI might randomly increase timeout limits, delete components, or rewrite your fetch logic without knowing *why* it's failing.

### ✅ The Good Prompt (Root Cause Analysis)
> "The `/api/generate` endpoint returns a 504 Gateway Timeout after approximately 30 seconds in production.
> 
> **Expected:** The request should complete successfully and return the JSON payload.
> **Environment:** Vercel serverless function.
> **Recent change:** Added a second external API request to Gemini.
> **Logs:** [Paste exact error log]
> 
> Analyze the likely root cause first. Do not modify code until you identify the bottleneck."

## The Structured Debugging Loop

When something breaks, force the AI to follow this exact loop:

1. **Reproduce:** Can we trigger the error consistently?
2. **Isolate:** Which specific file, function, or API endpoint is throwing the error?
3. **Diagnose:** What is the actual underlying failure? (e.g., "The API key is undefined on the server side.")
4. **Propose:** What is the narrowest possible fix?
5. **Implement & Test:** Apply the fix and verify.

If you enforce this structure, you will eliminate 90% of AI-induced bugs.
