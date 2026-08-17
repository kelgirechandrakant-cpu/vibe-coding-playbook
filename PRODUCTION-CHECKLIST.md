# The Production Checklist

AI coding agents are heavily biased towards making things work *locally*. A prototype that runs flawlessly on your laptop can immediately crash, leak data, or cost you thousands of dollars when exposed to the public internet.

Before you deploy your AI-generated app to production, run through this practical baseline checklist. *(Note: These checks do not guarantee 100% production safety, but they prevent the most common catastrophic failures).*

## 1. Functionality
- [ ] **Core flows work:** Can a user actually sign up, use the main feature, and log out?
- [ ] **Error states work:** If an API fails, is there a graceful UI message instead of a white screen of death?
- [ ] **Empty states work:** If a user has no data, is there a clear CTA to create some?
- [ ] **Loading states work:** Are buttons disabled while submitting to prevent double-charging?

## 2. Security
- [ ] **Secrets are not committed:** Check your git history. No `.env` files with real keys.
- [ ] **API keys are protected:** Ensure backend keys (OpenAI, Stripe) are not leaked to the frontend bundle (e.g., no `VITE_OPENAI_KEY`).
- [ ] **Authorization is checked:** Are database rules (RLS) enforcing that users can only read/write their own data?
- [ ] **User input is validated:** Is user-generated content sanitized before rendering (e.g., `DOMPurify`) to prevent XSS?
- [ ] **Sensitive data is handled correctly:** Are you accidentally logging passwords or PII to your server console?

## 3. Performance
- [ ] **Unnecessary requests removed:** Are you fetching the entire user list on the homepage by accident?
- [ ] **Large assets optimized:** Are images compressed? Is the AI importing massive libraries when native JS would work?
- [ ] **Slow operations identified:** Are you doing heavy processing on the main thread?
- [ ] **API timeouts considered:** If the LLM takes 40 seconds to reply, will your serverless function timeout at 10 seconds?

## 4. Frontend
- [ ] **Mobile responsive:** Did you actually test it on a phone screen, or just resize your desktop browser?
- [ ] **Accessibility checked:** Can you navigate the core flow using only the `Tab` key? Do buttons have `aria-labels`?
- [ ] **Browser behavior checked:** Does the UI break on Safari even if it works on Chrome?
- [ ] **UI states verified:** Are hover, active, and focus states clear?

## 5. SEO
- [ ] **Metadata:** Are `<title>` and `<meta description>` set correctly on public pages?
- [ ] **Sitemap:** Do you have a `sitemap.xml`?
- [ ] **Robots configuration:** Is `robots.txt` allowing crawlers (and not blocking the whole site)?
- [ ] **Canonical URLs:** Are they set where appropriate?
- [ ] **Structured data:** Is Schema.org JSON-LD added for articles or products?
- [ ] **Indexability checked:** Is the content rendered server-side or statically, rather than hiding behind a client-side loading spinner?
- [ ] Programmatic/templated pages have genuinely unique content per page, not boilerplate with swapped variables (thin-content risk)
- [ ] Reciprocal hreflang tags are present on both sides of any translated page pair

## 6. Deployment
- [ ] **Environment variables configured:** Are production secrets added to Vercel/Netlify/AWS?
- [ ] **Production build tested:** Does `npm run build` actually succeed locally?
- [ ] **Logs available:** Do you have basic tracking or error logging (e.g., Vercel Logs, Sentry)?
- [ ] **Error monitoring considered:** How will you know if the app goes down?
- [ ] **Domain configured:** Is SSL provisioned and routing correctly?
