---
name: security-audit
description: "Security audit methodology. OWASP Top 10 + STRIDE threat model with zero-noise false positive filtering. Checks API key exposure, database rules, XSS vectors, CSRF, auth bypass. Use when handling user data or preparing for production."
---

# Security Audit Protocol

When invoked for a security review, execute a zero-noise audit focusing on real, exploitable vulnerabilities in modern web applications.

## 1. Authentication & Authorization Bypass
- Are protected routes actually checking user session tokens on the server, or just hiding UI elements on the client?
- Is Row-Level Security (RLS) or database rules (e.g., Firestore `allow read, write: if request.auth != null`) enforced properly?

## 2. Secrets Management
- Are any API keys (Stripe, OpenAI, Supabase) prefixed with `VITE_`, `NEXT_PUBLIC_`, or `REACT_APP_` by mistake?
- Are secrets committed to source control?

## 3. Data Validation & XSS
- Are we using `dangerouslySetInnerHTML`? If so, is the input passing through a sanitizer like DOMPurify first?
- Are backend API endpoints validating the shape and type of the request body, or blindly inserting it into the database?

## 4. Rate Limiting & Abuse
- Do expensive API routes (e.g., AI generation, email sending) have IP-based or User-based rate limiting?
- Is there protection against basic brute-forcing on login routes?

## Output
Report only actionable vulnerabilities. Discard theoretical warnings that do not apply to the current architecture. Provide the exact code snippet required to patch the vulnerability.
