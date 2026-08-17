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

## The Lesson
AI accelerates implementation, but it will always choose the path of least resistance (patching a symptom). The developer must act as the Senior Engineer, enforcing architectural boundaries and rejecting lazy patches.
