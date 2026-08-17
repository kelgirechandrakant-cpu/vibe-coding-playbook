---
name: plan-review
description: "Architecture and engineering review protocol. Locks architecture, data flow, edge cases, and test plans before coding. Forces hidden assumptions into the open. Use before building new features or making structural changes."
---

# Plan Review Protocol

Before writing code for a new feature, you must review the user's plan and lock down the architecture.

## 1. Trace the Data Flow
Analyze how data moves through the proposed feature:
- Where does the data originate?
- How is it mutated?
- Where is it stored?

## 2. Identify Edge Cases
List at least 3 failure states for the proposed architecture:
- What happens if the network fails midway?
- What if the user has stale data in their cache?
- What if the database rejects the schema?

## 3. Technology Alignment
Verify that the proposed solution aligns with the existing stack. If the user proposes adding a new dependency (e.g., Redux, Lodash), push back and ask if native APIs (Context, standard JS) can handle it.

## 4. Output the Architecture Lock
Produce a markdown block summarizing the final architecture, required files, and exactly what is **Out of Scope** for this PR. Request explicit approval before proceeding to implementation.
