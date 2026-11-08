# Case Study: PPT Maker (Student Suite)

This case study documents the honest journey of building [PPT Maker](https://pptmaker.co.in) (Student Suite) using AI coding agents. It highlights where the methodology worked, and more importantly, where it failed when the developer ceded too much control.

---

## Part 1: The Prototype to Initial Launch (June – August 2026)

### 1. The Idea
The goal was to build a web application that generates AI-powered presentation slides, exports them to `.pptx`, and provides premium templates for students. 

### 2. The Failure (Architecture Drift)
Initially, the developer asked the AI to "Build the premium template system." 

**What went wrong:**
- The AI generated a massive `SlideGenerator.tsx` file that tried to handle fetching the AI prompt, parsing the JSON, rendering the React preview, and exporting the PPTX file.
- When a bug occurred in the PPTX export, the developer said "Fix the export." 
- The AI patched the export logic but accidentally broke the React preview logic. 
- The developer entered the **Infinite Debugging Loop**.

### 3. The Diagnosis & Solution (The Theme Triad)
The developer stopped the AI and stepped back to evaluate the architecture. They realized the single monolith file was fundamentally flawed. 

They designed a new architecture: **The Theme Triad**. Every theme must have exactly three synchronized files:
1. `src/utils/gemini{Theme}.ts` (Prompt Engine)
2. `src/components/slides/{Theme}SlideRenderer.tsx` (Browser Preview)
3. `src/lib/ppt{Theme}.ts` (PPTX Exporter)

By forcing the AI to conform to this specific architecture across 25+ presentation themes, the infinite debugging loop ended. When the export broke, the developer pointed the AI *only* at `ppt{Theme}.ts`. 

### 4. 504 Timeouts & Rate Limits
**Problem:** The Gemini API would sometimes take 30+ seconds to respond. The Vercel serverless function timed out, throwing a 504 error. The AI suggested increasing the Vercel timeout limits (which costs money on higher tiers).

**Solution:** The developer pushed back on the AI's patch. Instead of paying for higher limits, they implemented a multi-key rotation system (`api-rotation/`) and streamed the response directly to the client to keep the connection alive. 

### 5. Alert Noise & Telemetry Safeguards
**Problem:** The developer set up an automated Telegram bot to alert on tool failures. However, when guest users uploaded corrupted `.docx` or non-zip files, JSZip threw raw errors (`Can't find end of central directory`), flooding the developer's Telegram alerts with false alarms.

**Solution:** Instead of treating user-side input errors as critical system failures, the developer updated `toolTelemetry.ts` to filter out benign error regex patterns (corrupted zips, user cancels, network aborts) while wrapping file extractors in friendly UI error fallbacks. This restored high signal-to-noise ratio in production alerts.

### 6. Acquiring 3,000 Users via Programmatic AI SEO
**Problem:** The app was functional, but zero people were visiting it. The developer knew SEO was the best long-term acquisition channel, but manually coding dozens of landing pages and embedding schema would take months.

**Solution:** Instead of asking the AI to "write a blog post," the developer created rigid "Agent Skills" (`add-landing`, `add-blog`) to instruct the AI how to generate SEO-optimized React pages systematically:
1. **Schema Automation:** The AI was constrained to automatically inject valid JSON-LD schemas (FAQ, SoftwareApplication) into the `<head>` of every generated page.
2. **Programmatic Architecture:** The AI was directed to build dynamic URL structures (`/templates/:slug`, `/vs/gamma`, `/vs/canva`) to capture long-tail keywords.
3. **Core Web Vitals Protection:** The AI was routinely audited using a `perf-audit` protocol to ensure it didn't bloat the bundle size with heavy libraries.

**The Initial Real-World Results (June - August 2026):**
- **75% of traffic is non-branded:** The homepage accounted for only 24% of views; programmatic SEO drove the rest.
- **High-Intent Landing Pages:** The `/ai-ppt-generator` URL alone drove 1,324 views, 510 active users, and **424 conversions**.
- **Long-Tail Dominance:** Programmatic competitor pages (`/vs/gamma`, `/vs/canva`) and niche template URLs captured high-intent search traffic without ad spend.

---

## Part 2: Scaling from Prototype to Student Suite (August – November 2026)

As traffic grew, the single presentation generator evolved into **Student Suite** — integrating a Mobile Presentation Studio, Dual-Mode ATS Resume Builder, and Client-Side PDF Tools. Here is how vibe coding scaled across a complex multi-product platform without collapse.

### 7. The Mobile Reality Check: Responsive CSS vs. Touch Architecture
**Problem:** When asked to "make the presentation editor work on mobile," the AI took the path of least resistance: applying `hidden sm:block`, shrinking fonts, and stacking controls vertically.
- The 16:9 slide canvas shrunk to an illegible 180px thumbnail on phones.
- Small buttons ($24\text{px}$) caused constant mis-clicks.
- Editing text required scrolling through endless desktop sidebars.

**Solution (The Developer Intervened):**
Instead of letting the AI guess responsive CSS, the developer designed three strict engineering constraints:
1. **Mathematical Stage Containment:** Implemented a non-negotiable containment formula:
   ```typescript
   fitScale = Math.min((containerWidth - 32) / 1280, (containerHeight - 32) / 720, 1.0);
   ```
   This guaranteed the 16:9 stage (1280×720) scales proportionally into any phone, tablet, or desktop viewport without distortion.
2. **WCAG 2.2 AAA Touch Targets:** Enforced a rule that all mobile buttons, sheet toggles, and inspection controls must have a minimum hit area of $\ge 44 \times 44\text{ CSS px}$.
3. **Mobile-Native Sheet Pattern:** Replaced desktop sidebars with a bottom `MobileEditSheet` for thumb reach and added a `SlideInspectionOverlay` allowing 100%–200% pinch zoom.

### 8. Multi-Pillar State Isolation (The Career Context Bridge)
**Problem:** When expanding into ATS Resumes, Cover Letters, and Interview Prep, the AI tried to combine everything into a monolithic global context. Modifying a resume field began triggering unnecessary re-renders in the presentation editor and corrupted shared local storage.

**Solution:** The developer architected a decoupled state pattern:
- **`careerStateBridge.ts`**: A dedicated, lightweight state bridge that stores only active job target metadata (company, target role, JD keywords).
- **`ApplicationContextBar.tsx`**: A persistent banner across career tools that shares target job context without coupling the underlying tool components.
- Each tool (Resume Builder, Cover Letter AI, Mock Interview) operates 100% independently in standalone mode if no context is set.

### 9. On-Demand Dynamic Code-Splitting (~410 KB Gzip Saved)
**Problem:** As themes expanded from 15 to 28+ triads, bundling all prompt parsers, slide renderers, and PptxGenJS exporters into the main bundle caused initial bundle size to explode, destroying mobile First Contentful Paint (FCP) and Google Lighthouse scores.

**Solution:** The developer restructured theme registration into `themeRegistry.ts` using dynamic asynchronous imports:
```typescript
const { downloadMinimalPPT } = await import('../lib/pptMinimal');
```
Theme renderers and PowerPoint exporters are loaded over the wire only when the user selects that specific theme. This saved **~410 KB gzip** from the initial bundle.

### 10. The Automated Regression Shield (47 Suites / 298 Vitest Tests)
**Problem:** With 28+ themes and 3 major product suites, every time the AI was asked to modify a prompt or fix a styling bug, it risked introducing regressions in exports or normalizer logic.

**Solution:** The developer instituted an unbreakable development law: **No PR is merged unless all automated test suites pass.**
- Created a comprehensive Vitest test harness covering:
  - Theme triad synchronicity (verifying prompts, renderers, and exporters match data shapes).
  - Normalizer invariants (`slideNormalizer.ts` filtering junk bullets).
  - Dynamic luminance contrast defense (preventing unreadable white-on-white text).
  - Security defense (auto-jailing SQLi/XSS payloads, rate limiting, and origin defense).
- The test suite expanded to **47 test suites and 298 passing tests**, executing in under 8 seconds. If an AI change causes a single failure, it is rejected immediately.

---

## The Master Lesson of Vibe Coding

AI accelerates implementation by 10x, but its natural gravity is toward **architectural entropy** — monolithic files, symptom-patching, and bloated bundles.

To succeed with AI coding agents:
1. **You are the Architect:** Define the modular boundaries (Theme Triads, State Bridges, Containment Formulas).
2. **Force Strict Verification:** Use automated test suites (Vitest, Playwright) as a physical shield against regression.
3. **Constrain the Scope:** Never allow an AI to touch more than 2–3 files in a single prompt.
4. **Optimize for Real Users:** Test exports in real viewers (PowerPoint, Google Slides) and real phones, not just desktop browser previews.
