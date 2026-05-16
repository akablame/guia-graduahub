---
name: vercel-react-best-practice
description: React and Next.js performance optimization guidelines from Vercel Engineering. Use when writing, reviewing, or refactoring React/Next.js code to ensure optimal performance patterns.
license: MIT
metadata:
  author: vercel
  version: "1.0.0"
---

# Vercel React Best Practices

Comprehensive performance optimization guide for React and Next.js applications, maintained by Vercel. Contains 70 rules across 8 categories, prioritized by impact.

## When to Apply

Reference these guidelines when:
- Writing new React components or Next.js pages
- Implementing data fetching (client or server-side)
- Reviewing code for performance issues
- Refactoring existing React/Next.js code
- Optimizing bundle size or load times

## Rule Categories by Priority

| Priority | Category | Impact |
|----------|----------|--------|
| 1 | Eliminating Waterfalls | CRITICAL |
| 2 | Bundle Size Optimization | CRITICAL |
| 3 | Server-Side Performance | HIGH |
| 4 | Client-Side Data Fetching | MEDIUM-HIGH |
| 5 | Re-render Optimization | MEDIUM |
| 6 | Rendering Performance | MEDIUM |
| 7 | JavaScript Performance | LOW-MEDIUM |
| 8 | Advanced Patterns | LOW |

## Quick Reference

### 1. Eliminating Waterfalls (CRITICAL)
- Check cheap sync conditions before awaiting flags or remote values
- Move await into branches where actually used
- Use Promise.all() for independent operations
- Start promises early, await late in API routes

### 2. Bundle Size Optimization (CRITICAL)
- Import directly, avoid barrel files
- Use next/dynamic for heavy components
- Load analytics/logging after hydration
- Load modules only when feature is activated

### 3. Server-Side Performance (HIGH)
- Authenticate server actions like API routes
- Use React.cache() for per-request deduplication
- Minimize data passed to client components
- Use after() for non-blocking operations

### 4. Client-Side Data Fetching (MEDIUM-HIGH)
- Use SWR for automatic request deduplication
- Deduplicate global event listeners
- Use passive listeners for scroll

### 5. Re-render Optimization (MEDIUM)
- Extract expensive work into memoized components
- Use primitive dependencies in effects
- Use functional setState for stable callbacks
- Use startTransition for non-urgent updates

### 6. Rendering Performance (MEDIUM)
- Use content-visibility for long lists
- Extract static JSX outside components
- Use Activity component for show/hide
- Use React DOM resource hints for preloading

### 7. JavaScript Performance (LOW-MEDIUM)
- Build Map for repeated lookups
- Cache function results in module-level Map
- Return early from functions
- Use Set/Map for O(1) lookups

### 8. Advanced Patterns (LOW)
- Store event handlers in refs
- Initialize app once per app load
- useLatest for stable callback refs
