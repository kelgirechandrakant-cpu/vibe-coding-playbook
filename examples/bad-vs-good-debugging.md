# Bad vs. Good Debugging

The difference between a successful vibe coder and someone trapped in an "Infinite Debugging Loop" is how they respond to errors. 

## Scenario: React State is Stale

You click a button to delete an item from a shopping cart, but the total price at the top of the screen doesn't change.

### ❌ The Bad Workflow
**Developer:** "The total price isn't updating when I delete an item. Fix it."
**AI:** "Sorry about that! Let me fix it." (AI rewrites the entire `CartContext.tsx` using `useReducer` instead of `useState`, which breaks the "Add to Cart" function).
**Developer:** "Now Add to Cart is broken! Fix that."
**AI:** "Sorry!" (AI adds a `useEffect` loop that crashes the browser).

**Why it fails:** The developer did not isolate the bug. The AI guessed the solution and patched a symptom.

### ✅ The Good Workflow
**Developer:** "In `CartContext.tsx`, when `removeItem(id)` is called, the item is removed from the array successfully, but the `totalPrice` variable does not recalculate. Formulate a hypothesis."
**AI:** "Hypothesis: You might be mutating the array directly using `.splice()` or `.push()`, which doesn't trigger a React re-render. We should use `.filter()` to create a new array reference."
**Developer:** "Yes, I see a `.splice()` on line 42. Fix just that line to use `.filter()`."

**Why it works:** The developer forces the AI to form a hypothesis before generating code, and restricts the AI to the narrowest possible fix.

---

## Scenario: Backend API 500 Error

### ❌ The Bad Workflow
**Developer:** "I'm getting a 500 error from the backend. Fix it."
**AI:** "I will add a `try/catch` block to the frontend to suppress the error."

**Why it fails:** Suppressing an error on the frontend does not fix the backend crash.

### ✅ The Good Workflow
**Developer:** "The frontend is receiving a 500 Internal Server Error when calling `/api/users`. Here is the exact backend terminal log: `TypeError: Cannot read properties of undefined (reading 'email')`. 
Locate the file responsible for this route and tell me which line is likely failing."

**Why it works:** The developer provides the exact log and isolates the layer (backend route). The AI is directed to investigate, not patch.
