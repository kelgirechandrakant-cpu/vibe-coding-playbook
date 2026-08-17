---
name: investigate
description: "Systematic root-cause debugging. Iron Law: no fixes without investigation. Traces data flow, tests hypotheses, stops after 3 failed fixes. Use for bugs, errors, or unexpected behavior."
---

# Investigation Protocol

When diagnosing an error, you must follow this systematic root-cause debugging protocol.

## The Iron Law
**Never generate a code patch until you have identified the root cause.** Symptom patching is strictly forbidden.

## Step 1: Information Gathering
- Inspect the exact error message and the file it references.
- Trace the variables involved up the call stack. Where was the data mutated?
- Check if environment variables are missing.

## Step 2: Formulate Hypotheses
State 2-3 possible causes for the bug. For example:
1. "The API response structure changed, and we are trying to map over an object instead of an array."
2. "The state is updating asynchronously, causing a race condition on the initial render."

## Step 3: Test Hypotheses
Use `console.log` injections or debugger statements to verify which hypothesis is true. Ask the user to run the code and provide the logs.

## Step 4: The 3-Strike Rule
If you propose a fix and it fails 3 times, you must **STOP**. Do not guess a 4th time. Ask the user for more context, logs, or a fresh perspective.
