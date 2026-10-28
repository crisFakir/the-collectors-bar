# The Collectors Bar

Online store for trading card games and collectibles, built around **live breaks on Twitch**. Based in Portugal, with a warehouse on Terceira Island (Azores).

> **Status:** planning — requirements and architecture in progress, no application code yet.

## About

The Collectors Bar sells:

- **Live breaks** — sealed booster boxes opened live on Twitch; buyers purchase packs and receive their cards.
- **Sealed product** — booster packs, boxes and starter decks.
- **Singles** — individual cards, graded and ungraded.
- **Figures and accessories** — Funko Pop, LEGO, sleeves, binders and more.

Highlights of the planned system:

- **Vault** — cards pulled in breaks are kept in the customer's vault and shipped together on request, paying shipping only once.
- **No overselling** — break spots and limited products stay consistent under the purchase spikes of a live stream.
- **Portuguese payments and invoicing** — MB WAY, Multibanco and card via Easypay; certified invoices via InvoiceXpress.
- **Bilingual** — Portuguese (pt-PT) and English.
- **Custom back office** — designed so that non-technical staff can manage products, breaks and shipments without training.

## Tech stack

| Layer | Choice | Decision |
|---|---|---|
| Framework | Next.js (App Router) | [ADR-0002](docs/adr/0002-use-nextjs-and-typescript.md) |
| Language | TypeScript (strict) | [ADR-0002](docs/adr/0002-use-nextjs-and-typescript.md) |
| Database, ORM, styling, hosting | To be decided | — |

## Documentation

- [Requirements](docs/requirements.md) — functional and non-functional requirements, glossary, open questions
- [Architecture Decision Records](docs/adr/README.md) — why the system is built the way it is

## Development workflow

- Work is planned as GitHub Issues (user stories grouped in epics) on the project board.
- Each change is made on its own branch and merged through a pull request with passing CI.
- Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/), e.g. `feat(checkout): enforce purchase limits`.

Setup instructions will be added with the first application code.

## License

Copyright © 2026 crisFakir. All rights reserved — see [LICENSE](LICENSE). The code is public for portfolio purposes only.
