---
name: ship
description: "Pre-deploy checklist and shipping automation. Verifies exports work, builds pass, and prepares for deployment. Use when ready to deploy, push, or create a PR."
---

# Shipping Protocol

When the user says they are ready to ship, deploy, or commit a major feature, execute this pre-flight sequence to prevent breaking production.

## 1. Build Verification
- Does the project actually compile? (`npm run build` or equivalent).
- Are there any unresolved TypeScript errors or missing imports?

## 2. Environment Verification
- Did we introduce new environment variables during development?
- If so, remind the user to add them to their production hosting provider (Vercel, AWS, etc.).

## 3. End-to-End Walkthrough
- Mentally simulate the user journey of the new feature.
- Is there a dead end where the user gets stuck without a "Back" or "Cancel" button?
- Does the feature gracefully handle the case where the user is completely logged out?

## Output
If all checks pass, output a summary of the changes and provide the exact Git commit command with a descriptive, conventional commit message (e.g., `git commit -m "feat: add user authentication"`).
