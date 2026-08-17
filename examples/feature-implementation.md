# Feature Implementation Workflow

This is a concrete example of how to implement a new feature using the Vibe Coding methodology. Notice how the developer breaks the work into verifiable increments.

## The Goal
Add a "Dark Mode" toggle to an existing React application.

## Phase 1: Planning (No Code Allowed)

**Developer Prompt:**
> "I want to add a Dark Mode toggle to my app. Currently, we use TailwindCSS. 
> Inspect `tailwind.config.js` and `App.tsx`. 
> Propose the simplest architecture for this feature. Do not write the implementation yet."

**AI Response:**
> Architecture Proposal:
> 1. Update `tailwind.config.js` to use `darkMode: 'class'`.
> 2. Create a `ThemeProvider` context to store the user's preference in `localStorage`.
> 3. Wrap `App.tsx` in this provider.
> 4. Create a `<ThemeToggle />` button component.

## Phase 2: Implementation (Incremental)

**Developer Prompt:**
> "The architecture is approved. Let's do Step 1 and 2 only. 
> Update the Tailwind config, and generate the `ThemeProvider.tsx` file. Ensure it checks the user's system preference by default."

*(AI generates code. Developer inspects the code, runs the app locally, and commits the change).*

**Developer Prompt:**
> "Step 1 and 2 are committed and working. Now do Step 3 and 4. 
> Wrap `App.tsx` and generate the `<ThemeToggle />` component. Make it a simple moon/sun icon button."

## Phase 3: Verification

**Developer Action:**
The developer clicks the button in the browser. It works. They refresh the page. The dark mode state persists (because of `localStorage`). 

**Developer Prompt:**
> "The feature is working. Run a quick code review on `ThemeProvider.tsx` and `<ThemeToggle />`. Are there any performance issues with the context provider?"

**AI Response:**
> "The context provider is clean. However, to prevent a flash of unstyled content (FOUC) on initial load, you should add a small blocking script to `index.html`."

**Developer Prompt:**
> "Good catch. Generate that script for `index.html`."

## The Result
By splitting the work into Planning, Incremental Implementation, and Verification, the developer avoided massive monolithic PRs and prevented the AI from breaking existing CSS.
