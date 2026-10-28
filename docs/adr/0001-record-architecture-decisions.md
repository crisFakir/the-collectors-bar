# ADR-0001: Record architecture decisions

- **Status:** Accepted
- **Date:** 2026-10-28
- **Related requirements:** NFR-DOC-01

## Context

This project is both a real store and a public portfolio. Decisions about frameworks, data storage, providers and architecture need to be understandable by future contributors and by reviewers of the repository, who will ask not only *what* was chosen but *why*.

## Options considered

1. **No formal record** — decisions live in chat, Jira or memory.
   - Pros: no overhead.
   - Cons: context is lost; decisions get re-discussed; not visible to repository readers.
2. **Wiki or external tool** (Confluence, Notion).
   - Pros: rich editing.
   - Cons: separated from the code; not versioned with it; may not be public.
3. **ADRs as Markdown files in the repository** (`docs/adr/`).
   - Pros: versioned with the code; reviewed through pull requests; readable on GitHub.
   - Cons: requires discipline to keep writing them.

## Decision

We will record significant technical decisions as ADRs in `docs/adr/`, using the template in `0000-template.md` and the process described in `docs/adr/README.md`.

## Consequences

- Every significant decision gets a numbered, immutable record.
- Changing a decision means writing a new ADR that supersedes the old one, preserving history.
- Pull requests that introduce a significant decision should include its ADR.
