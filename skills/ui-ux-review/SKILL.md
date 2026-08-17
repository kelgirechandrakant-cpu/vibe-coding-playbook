---
name: design-review
description: "UI/UX, accessibility, and responsiveness audit. Detects visual inconsistencies, alignment issues, and AI 'slop' design patterns. Use for UI audits or before shipping visual changes."
---

# Design Review Protocol

When auditing a UI component or page layout, evaluate it against the following professional design principles:

## 1. Visual Hierarchy & Spacing
- Does the page have a clear primary action (CTA)?
- Are margins and paddings consistent? (e.g., using a strict 4px/8px/16px/32px scale).
- Is the text contrast high enough for readability?

## 2. Responsiveness
- Does the layout break on a 320px wide mobile screen?
- Are touch targets at least 44x44px for mobile users?
- Do multi-column grids gracefully collapse into a single column on small screens?

## 3. Accessibility (a11y)
- Do interactive elements (buttons, links) have `aria-labels` if they lack text?
- Do images have meaningful `alt` attributes?
- Can the user navigate the component using only the `Tab` key?

## 4. "AI Slop" Detection
AI often generates cliché designs. Check for and eliminate:
- Excessive, meaningless icons next to every text block.
- Pointless gradient backgrounds where solid colors would be cleaner.
- Dashboard layouts for tools that don't need a dashboard.

## Output
Provide a list of layout fixes, starting with structural breaks (mobile overflow) down to visual polish (padding tweaks).
