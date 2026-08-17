# The Production Checklist

AI coding agents are heavily biased towards making things work *locally*. A prototype that runs flawlessly on your laptop can immediately crash, leak data, or cost you thousands of dollars when exposed to the public internet.

Before you deploy your AI-generated app to production, run through this checklist.

## 1. Security & Authentication
- [ ] **API Keys Hidden:** Are all sensitive API keys (OpenAI, Gemini, Stripe) stored in backend environment variables (`.env`) and NOT exposed to the frontend browser bundle?
- [ ] **Database Rules Locked:** If using Firebase, Supabase, or similar, are the security rules configured so users can only read/write their *own* data?
- [ ] **Rate Limiting:** Is there a rate limiter (e.g., `express-rate-limit` or Upstash) on your expensive API routes to prevent a single user from running up your AI billing?
- [ ] **Input Sanitization:** Is user-generated content sanitized before rendering to prevent XSS attacks? (e.g., using `DOMPurify`).

## 2. Error Handling & Edge Cases
- [ ] **API Failures:** If the LLM API times out or returns a 500 error, does the UI show a graceful error message, or does the entire app crash?
- [ ] **Empty States:** If a user has no data yet, is there a friendly empty state and a clear CTA?
- [ ] **Loading States:** Are there visual indicators (spinners, skeletons) while heavy asynchronous AI tasks are running?

## 3. Performance & SEO
- [ ] **Mobile Responsiveness:** Have you actually tested the UI on a real mobile device viewport, or just resized your browser?
- [ ] **Meta Tags:** Are the `<title>`, `<meta description>`, and Open Graph images set up for social sharing?
- [ ] **Bundle Size:** Did the AI accidentally import a massive library (like `lodash` or `moment`) when a native JavaScript function would suffice?

## 4. Deployment
- [ ] **Production Environment Variables:** Have you added the necessary production secrets to your hosting provider (Vercel, Netlify, Render)?
- [ ] **Analytics/Logging:** Do you have basic tracking (Vercel Analytics, Google Analytics, PostHog) set up to see if people are actually using the app?
- [ ] **Custom Domain Setup:** Is SSL provisioned and routing correctly?

> **Rule of Thumb:** Never let an AI auto-deploy to production without a human reviewing the `git diff`.
