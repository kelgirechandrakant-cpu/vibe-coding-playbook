---
name: anti-slop-ui
description: Enforces human design standards and prevents generic AI styling patterns in frontend code.
---

# Anti-Slop UI & Frontend Taste Skill

When generating frontend components, AI coding agents default to generic, low-effort aesthetics: washed-out purple/indigo gradients, floating low-contrast cards, and broken mobile hit targets.

Follow these rules to produce interfaces that look engineered by a human product designer:

## 1. Typography & Hierarchy
- **No generic font stacks:** Avoid defaulting to Inter everywhere. Use intentional, editorial, or clean monospace font hierarchies where appropriate.
- **Strict Scale Contrast:** Make section titles decisively distinct from body text.
- **Comfortable Line Height:** Body text should maintain `leading-relaxed` (1.6 to 1.7) and line length between 60–75 characters.

## 2. Color & Contrast Defense
- **Banned:** Multi-colored radial gradients behind dark text.
- **WCAG Compliance:** Always verify text-to-background contrast ratio ($\ge 4.5:1$ for normal text, $\ge 3:1$ for large text).
- **Restrained Palettes:** Stick to a single primary brand color, a dark neutral (`slate-900` / `zinc-900`), and a light neutral (`slate-50` / `zinc-50`). Use accent colors sparingly for primary calls to action.

## 3. Mobile-First Interaction
- **Touch Target Law:** Every clickable button, drawer toggle, and icon link must have a minimum touch target of $\ge 44 \times 44\text{ CSS pixels}$ (WCAG 2.2 AAA / Apple HIG).
- **Thumb-Zone Controls:** On mobile screens ($< 768\text{px}$), use bottom-sheet drawers (`MobileEditSheet`) instead of cramped sidebars.
- **Stage Containment:** When displaying fixed-aspect-ratio canvases (e.g. 16:9 slides, video players, A4 documents), never let them stretch or clip:
  ```typescript
  fitScale = Math.min((containerWidth - 32) / baseWidth, (containerHeight - 32) / baseHeight, 1.0);
  ```

## 4. Animation Without Layout Shift (CLS)
- Animate only `transform` and `opacity`.
- Never animate `width`, `height`, `top`, `left`, or `margin` during user interaction, as this forces browser layout recalculation.
