# Workflow Prompts

Stop using generic prompts like *"Build me a modern dashboard with React and Firebase."* 
Use these highly structured workflow prompts to maintain control of the AI and force it to think before it writes code.

---

## 1. Planning Phase

### Onboarding AI to an Existing Codebase
*Why it works: Prevents the AI from hallucinating a stack, architecture, or naming convention by forcing it to read the current reality first.*

```text
Before we start building anything, I need you to understand this project.
1. Inspect the root folder structure and the primary source directories.
2. Identify the authentication pattern being used (if any).
3. Identify the data fetching layer or database pattern.
4. Summarize the existing naming and styling conventions (e.g., CSS modules vs Tailwind).

Do not write any code. Just output your summary of the project's current state so I can confirm you understand it.
```

### Project Discovery & Architecture
*Why it works: Forces the AI to design the system, data models, and edge cases before generating spaghetti code.*

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

## 2. Implementation Phase

### Implement a Feature
*Why it works: Constrains the AI to the agreed-upon plan and forces it to inspect existing code rather than hallucinating paths.*

```text
Based on our approved plan, we will now implement Step 1: [Specific Task].

Please:
1. Inspect the existing code in [Folder/File Path].
2. Identify which files need to be modified.
3. Write the implementation for this specific step.
4. Ensure you include error handling for [Specific Failure State].

Keep the change as narrow as possible. Do not modify files outside of this scope.
```

### Refactoring a Component
*Why it works: Prevents the AI from accidentally changing the functionality while it cleans up the structure.*

```text
The file [Filename] has become too complex and messy.
I want to refactor it into smaller, more maintainable pieces.

CRITICAL RULE: We are changing the structure, NOT the functionality. The end-user experience must remain exactly identical.

First, identify the 3-4 distinct responsibilities this file currently handles.
Then, propose a folder structure and component breakdown for the refactor.
Wait for my approval before modifying the code.
```

## 3. Debugging Phase

### Structured Bug Investigation
*Why it works: Stops the "Infinite Debugging Loop" by forcing the AI to identify the root cause instead of patching the symptom.*

```text
The [API Endpoint / Component] is throwing the following error:
[Paste exact error log]

Environment: [Local / Production / Vercel]
Recent change: [What did you just modify?]

Do not immediately generate a code patch. 
1. Formulate a hypothesis for the root cause.
2. Identify the specific file/layer where this is failing.
3. Tell me what `console.log` or test I should run to confirm your hypothesis.
```

## 4. Review Phase

### Pre-Commit Code Review
*Why it works: Acts as an automated senior engineer looking over your PR before you merge.*

```text
Review the code changes you just generated for [Feature Name] against the following criteria:
1. Security: Are there any obvious vulnerabilities (e.g., exposed API keys, lack of authorization checks)?
2. Performance: Does this introduce any infinite loops, massive re-renders, or heavy bundle additions?
3. Maintainability: Is this hardcoded, or is it scalable?

If there are issues, list them. If it is clean, give me the exact command to run a local test.
```

### Security Audit
*Why it works: Explicitly triggers a strict threat model review against a specific surface area before shipping to production.*

```text
Run the `security-audit` skill against [Route / File Path]. 
Specifically check for XSS vectors, CSRF vulnerabilities, and Firebase security rules / RLS bypasses. 
Do not output generalized advice. Tell me exactly what vulnerabilities exist in this specific code and how to fix them before deployment.
```
