# Bad vs. Good Prompts

To control an AI, you must stop treating it like a magic wand and start treating it like a junior developer who needs strict boundaries.

## Scenario: Building an Authentication System

### ❌ The Bad Prompt
> "Build authentication for my application using Firebase. I need login, signup, and protected routes."

**Why it fails:**
The AI will generate 5 massive files at once. It might use outdated Firebase v8 syntax. It might wrap your entire app in a heavy Context provider that causes unnecessary re-renders. If it fails, you won't know which part is broken.

### ✅ The Good Prompt
> "First, inspect the existing architecture in `src/App.tsx` and identify how routing is currently handled. Then, propose the smallest architectural implementation required for email/password authentication using Firebase v10. Do not write the code yet. Just outline the files you will create and the data flow."

**Why it works:**
1. It forces the AI to read the existing context before acting.
2. It explicitly states the version (v10).
3. It separates the **Architecture** phase from the **Implementation** phase, giving you veto power before code is written.

---

## Scenario: Refactoring a Messy Component

### ❌ The Bad Prompt
> "Clean up `Dashboard.tsx`, it's too long."

**Why it fails:**
The AI will delete code it doesn't understand, break your CSS, and introduce new bugs while attempting to "clean" the file.

### ✅ The Good Prompt
> "The file `Dashboard.tsx` is 800 lines long. I want to refactor it.
> CRITICAL RULE: We are changing the structure, NOT the functionality. The end-user experience must remain exactly identical.
> 
> Identify the 3 distinct UI components inside this file that can be extracted into their own files. Propose the new folder structure. Wait for my approval."

**Why it works:**
It sets a strict boundary ("changing structure, not functionality") and breaks the refactor into an analytical step first.
