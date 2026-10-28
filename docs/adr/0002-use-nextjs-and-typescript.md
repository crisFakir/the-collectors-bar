# ADR-0002: Use Next.js and TypeScript for the whole application

- **Status:** Accepted
- **Date:** 2026-10-28
- **Related requirements:** NFR-SEO-01, NFR-PERF-01, NFR-MAINT-02, I18N-02

## Context

We need a storefront, a back office and a backend (payments, invoicing, shipping, breaks). Constraints:

- One developer, with experience in JavaScript, PHP, Java and C#, starting to learn React.
- Product and category pages must rank well in search engines, so they must be rendered on the server.
- The UI must be modern and dynamic (live break status, spots selling in near real time).
- Low running costs and a fast path to go-live.

## Options considered

1. **Next.js (React) full-stack, in TypeScript** — one project for storefront, back office and server logic (Server Components, Server Actions, Route Handlers).
   - Pros: server rendering and routing built in; one language end to end; large ecosystem and job market; first-class i18n routing support.
   - Cons: the framework evolves fast; server/client boundaries need to be learned.
2. **React SPA (Vite) + separate backend in Java/Spring Boot or .NET**
   - Pros: reuses existing Java/C# knowledge; strong backend frameworks.
   - Cons: a SPA renders in the browser, which hurts SEO; two projects, two languages and two deployments to maintain alone.
3. **React Router v7 (formerly Remix) full-stack**
   - Pros: server rendering, web-standards approach.
   - Cons: smaller ecosystem and fewer learning resources than Next.js.

## Decision

We will build the whole application with **Next.js (App Router)** and **TypeScript in strict mode**, organised as a **modular monolith**: one deployable application, internally split into modules that follow the requirement areas (catalogue, breaks, vault, checkout, payments, etc.).

## Consequences

- Shared types between frontend and backend: a change in the data model is caught by the compiler on both sides.
- Domain logic lives in plain TypeScript modules independent of Next.js, so it can be unit-tested and, if ever needed, moved to a separate service.
- The team must learn React Server Components and the server/client boundary.
- Database, ORM, hosting and styling are separate decisions, recorded in their own ADRs.
