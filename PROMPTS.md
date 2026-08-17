# Workflow Prompts

Stop using generic prompts like *"Build me a modern dashboard with React and Firebase."* 
Use these highly structured workflow prompts to maintain control of the AI and force it to think before it writes code.

---

## 1. The Architecture Framing Prompt
*Use this when starting a brand new feature to force the AI to design the system before writing code.*

```text
I want to build a [Feature Name] feature for my application.
Here is the objective: [Insert Objective]
Here is who it is for: [Target User]

Before writing any code, output a technical implementation plan covering:
1. User Flow: What happens step-by-step from the user's perspective?
2. Data Model: What database tables/collections and fields do we need?
3. Component Architecture: Which UI components will need to be created or modified?
4. Edge Cases: What are 3 ways this could fail, and how will we handle them?

Do not write any implementation code until I approve the plan.
```

## 2. The Implementation Prompt
*Use this after the architecture is approved to execute the plan in small steps.*

```text
Based on our approved plan, we will now implement Step 1: [Specific Task].

Please:
1. Inspect the existing code in [Folder/File Path].
2. Identify which files need to be modified.
3. Write the implementation for this specific step.
4. Ensure you include error handling for [Specific Failure State].

Keep the change as narrow as possible. Do not modify files outside of this scope.
```

## 3. The Code Review Prompt
*Use this after the AI writes code, but before you commit it.*

```text
Review the code changes you just generated for [Feature Name] against the following criteria:
1. Security: Are there any obvious vulnerabilities (e.g., exposed API keys, lack of authorization checks)?
2. Performance: Does this introduce any infinite loops, massive re-renders, or heavy bundle additions?
3. Maintainability: Is this hardcoded, or is it scalable?

If there are issues, list them. If it is clean, give me the exact command to run a local test.
```

## 4. The Refactor Prompt
*Use this when your codebase is getting messy, but you want to ensure the AI doesn't break functionality.*

```text
The file [Filename] has become too complex and messy.
I want to refactor it into smaller, more maintainable pieces.

CRITICAL RULE: We are changing the structure, NOT the functionality. The end-user experience must remain exactly identical.

First, identify the 3-4 distinct responsibilities this file currently handles.
Then, propose a folder structure and component breakdown for the refactor.
Wait for my approval before modifying the code.
```
