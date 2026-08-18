# Case Study: PPT Maker (Student Suite)

This case study documents the honest journey of building [PPT Maker](https://pptmaker.co.in) (Student Suite) using AI coding agents. It highlights where the methodology worked, and more importantly, where it failed when the developer ceded too much control.

## The Idea
The goal was to build a web application that generates AI-powered presentation slides, exports them to `.pptx`, and provides premium templates for students. 

## The Failure (Architecture Drift)
Initially, the developer asked the AI to "Build the premium template system." 

**What went wrong:**
- The AI generated a massive `SlideGenerator.tsx` file that tried to handle fetching the AI prompt, parsing the JSON, rendering the React preview, and exporting the PPTX file.
- When a bug occurred in the PPTX export, the developer said "Fix the export." 
- The AI patched the export logic but accidentally broke the React preview logic. 
- The developer entered the **Infinite Debugging Loop**.

## The Diagnosis & Solution (The Theme Triad)
The developer stopped the AI and stepped back to evaluate the architecture. They realized the single monolith file was fundamentally flawed. 

They designed a new architecture: **The Theme Triad**. Every theme must have exactly three synchronized files:
1. `gemini{Theme}.ts` (Prompt Engine)
2. `{Theme}SlideRenderer.tsx` (Browser Preview)
3. `ppt{Theme}.ts` (PPTX Exporter)

By forcing the AI to conform to this specific architecture, the infinite debugging loop ended. When the export broke, the developer pointed the AI *only* at `ppt{Theme}.ts`. 

## 504 Timeouts & Rate Limits
**Problem:** The Gemini API would sometimes take 30+ seconds to respond. The Vercel serverless function timed out, throwing a 504 error. The AI suggested increasing the Vercel timeout limits (which costs money on higher tiers).

**Solution:** The developer pushed back on the AI's patch. Instead of paying for higher limits, they implemented a multi-key rotation system (`api-rotation/`) and streamed the response directly to the client to keep the connection alive. 

## Acquiring 3,000 Users via Programmatic AI SEO
**Problem:** The app was functional, but zero people were visiting it. The developer knew SEO was the best long-term acquisition channel, but manually coding dozens of landing pages and embedding schema would take months.

**Solution:** Instead of asking the AI to "write a blog post," the developer created rigid "Agent Skills" (`add-landing`, `add-blog`) to instruct the AI how to generate SEO-optimized React pages systematically. 
1. **Schema Automation:** The AI was constrained to automatically inject valid JSON-LD schemas (FAQ, SoftwareApplication) into the `<head>` of every generated page.
2. **Programmatic Architecture:** The AI was directed to build a `ToolsHub` and dynamic URL structures (`/tools/resume-builder`, `/tools/cover-letter`) to capture long-tail keywords.
3. **Core Web Vitals Protection:** The AI was routinely audited using a `perf-audit` protocol to ensure it didn't bloat the bundle size with heavy libraries, which would penalize the site in Google rankings.

By combining the developer's structural SEO strategy with the AI's code generation speed, PPT Maker rapidly deployed dozens of highly-optimized landing pages, resulting in over 3,000 organic users.

**The Real-World Results (June - August 2026):**
- **75% of traffic is non-branded:** The homepage accounts for only 24% of views. The programmatic SEO engine drives the rest.
- **High-Intent Landing Pages:** The `/ai-ppt-generator` URL alone drove 1,324 views, 510 active users, and **424 conversions**.
- **Long-Tail Dominance:** Programmatic competitor pages (`/vs/gamma`, `/vs/canva`) and hyper-niche template URLs (`/resume-templates/software-engineer-resume`) successfully intercepted high-intent search traffic.
- **Top-of-Funnel Reach:** AI-generated blog posts like "Top Fonts for Professional Slides" acted as a wide net, capturing nearly 500 views on a single article.

## The Lesson
AI accelerates implementation, but it will always choose the path of least resistance (patching a symptom). The developer must act as the Senior Engineer, enforcing architectural boundaries, optimizing for distribution (SEO), and rejecting lazy patches.
