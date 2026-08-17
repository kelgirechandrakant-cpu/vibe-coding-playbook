---
name: perf-audit
description: "Performance and bundle size optimization protocol. Analyzes loading strategy, network patterns, and rendering bottlenecks. Produces prioritized fix recommendations. Use when pages feel slow or before shipping major features."
---

# Performance Audit Protocol

When asked to audit performance, evaluate the application across these three critical domains:

## 1. Bundle & Network Optimization
- Are heavy libraries (charts, 3D rendering, PDF generators) being lazy-loaded using dynamic imports (e.g., `React.lazy`)?
- Is the app downloading massive uncompressed images?
- Are API responses paginated or capped, rather than returning thousands of records at once?

## 2. Render Performance
- Is there unnecessary state residing at the top level of the component tree, causing the entire app to re-render on every keystroke?
- Are expensive calculations wrapped in `useMemo`?
- Are functions passed to child components wrapped in `useCallback` (when appropriate)?

## 3. Perceived Performance
- Do asynchronous actions have immediate optimistic UI updates?
- Are there skeleton loaders preventing layout shift (Cumulative Layout Shift) while data fetches?

## Output
Provide a diagnosis and the exact code refactors needed to eliminate the bottlenecks.
