# Architecture Decision Records

An **Architecture Decision Record (ADR)** is a short document that captures one significant technical decision: the context, the options considered, the choice made and its consequences.

## Why

Code shows *what* was built. ADRs explain *why*. They help future contributors (and our future selves) understand past decisions instead of guessing or repeating discussions.

## When to write one

Write an ADR when a decision:

- is hard or expensive to reverse (framework, database, hosting, payment provider);
- affects the structure of the system (module boundaries, data model conventions);
- was discussed and had real alternatives.

Small, easily reversible choices do not need an ADR.

## How

1. Copy [`0000-template.md`](0000-template.md) to `NNNN-short-title.md`, using the next number.
2. Fill it in with status **Proposed** and open a pull request.
3. Once agreed, change the status to **Accepted** and merge.
4. ADRs are never edited after acceptance. If a decision changes, write a new ADR and mark the old one as **Superseded by ADR-NNNN**.

## Index

| ADR | Title | Status |
|---|---|---|
| [0001](0001-record-architecture-decisions.md) | Record architecture decisions | Accepted |
| [0002](0002-use-nextjs-and-typescript.md) | Use Next.js and TypeScript for the whole application | Accepted |
| [0003](0003-use-plantuml-for-uml-diagrams.md) | Use PlantUML for UML diagrams | Proposed |
