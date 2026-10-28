# Requirements — The Collectors Bar

> **Status:** Draft v0.1 · **Last updated:** 2026-10-28
>
> This document lists *what* the system must do (functional requirements) and *how well* it must do it (non-functional requirements). It does not describe *how* it will be built — that belongs in the [Architecture Decision Records](adr/README.md).

## 1. Context

The Collectors Bar is an online store for collectibles based in Portugal, with a warehouse on Terceira Island (Azores). It sells:

- **Live breaks** of Trading Card Games (TCG), streamed on Twitch — the main channel at launch.
- **Sealed** TCG product (boosters, booster boxes, starter decks, etc.).
- **Singles** (individual cards), also sold on Cardmarket.
- **Figures** (Funko Pop, LEGO, etc.) and **accessories** (sleeves, binders, toploaders, etc.).
- **Auctions** of selected items (later release).

Primary market: Portugal (Mainland, Azores and Madeira). Secondary market: rest of the EU, then worldwide.

## 2. Glossary

| Term | Definition |
|---|---|
| **Break** | Live event in which sealed product is opened on stream. Buyers purchase *spots*; the cards pulled are allocated to spot holders according to the *break format*. |
| **Spot** | A purchasable share of a break (e.g. one pack, one slot, the whole box). |
| **Break format** | The rules mapping pulled content to spots (e.g. personal, pick-your-spot, random spot). |
| **Hit** | A valuable card pulled during a break. |
| **Sealed** | Unopened product. |
| **Single** | An individual card sold on its own, described by game, set, number, rarity, language and condition. |
| **Vault** | A customer's holding area for items they own but which have not been shipped yet (break pulls, items put on hold). |
| **Variant** | A purchasable version of a product with its own SKU, price and stock (e.g. size, edition, language). |
| **Purchase limit** | Maximum quantity of a product a single customer may buy within a period. |
| **Pre-order** | Purchase of a product before its release date, shipped when it arrives. |

## 3. Actors

| Actor | Description |
|---|---|
| **Visitor** | Anonymous user browsing the site. |
| **Customer** | Registered user who buys products and break spots. |
| **Breaker** | Staff member who runs breaks on stream and records results. |
| **Staff** | Back-office operator: products, orders, fulfilment. |
| **Admin** | Owner: everything Staff can do plus settings, users, finance. |
| **Payment gateway** *(external)* | Easypay — MB WAY, Multibanco, card. |
| **Invoicing system** *(external)* | InvoiceXpress — certified invoicing (AT). |
| **Carrier** *(external)* | Shipment creation, labels, tracking. |
| **Twitch** *(external)* | Live status, player embed, account linking. |
| **Email service** *(external)* | Transactional email delivery. |

## 4. Prioritisation and releases

Each requirement has a **MoSCoW** priority and a target **release**:

- **Must** — the store cannot go live without it.
- **Should** — important, but there is a workaround.
- **Could** — nice to have.
- **Won't** — explicitly out of scope for now.

| Release | Goal |
|---|---|
| **R1** | Go-live: catalogue, breaks + vault, checkout, payments, invoicing, shipping, back office, legal, PT/EN. |
| **R2** | Growth: auctions, wishlists, back-in-stock alerts, extra carriers. |
| **Later** | Ideas without a business case yet. |

## 5. Functional requirements

### 5.1 Catalogue and navigation (CAT)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| CAT-01 | The system supports the product types *Sealed*, *Single*, *Figure*, *Accessory* and *Break spot*, each with type-specific attributes. | Must | R1 |
| CAT-02 | A product can have variants, each with its own SKU, price, stock and images. | Must | R1 |
| CAT-03 | Categories form a tree of unlimited depth (e.g. *Bandai → Dragon Ball Super → Fusion World → FB04*), managed in the back office — not hard-coded. | Must | R1 |
| CAT-04 | Products carry filterable attributes (brand, franchise/IP, game, set, language, format) independent of the category tree. | Must | R1 |
| CAT-05 | The main menu (including mega menus) is configured in the back office. | Must | R1 |
| CAT-06 | Listing pages support filtering (facets) and sorting (price, newest, name). | Must | R1 |
| CAT-07 | Search with autocomplete across products, sets and categories. | Must | R1 |
| CAT-08 | Search tolerates typos and matches both PT and EN names. | Should | R1 |
| CAT-09 | Singles have: game, set, card number, rarity, language, condition (Cardmarket scale: MT, NM, EX, GD, LP, PL, PO) and optional grading (company + grade). | Must | R1 |
| CAT-10 | Product pages show stock status (in stock, low stock, out of stock, pre-order). | Must | R1 |
| CAT-11 | Prices are shown with VAT included and a legend stating it. | Must | R1 |
| CAT-12 | Pre-orders with expected release date. | Should | R1 |
| CAT-13 | The homepage is dynamic and managed from the back office: live-now banner, upcoming breaks, new arrivals, featured products, promotions. | Must | R1 |
| CAT-14 | Customers can subscribe to back-in-stock notifications. | Could | R2 |
| CAT-15 | Customers can keep a wishlist. | Could | R2 |

### 5.2 Live breaks and Twitch (BRK)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| BRK-01 | Staff creates a break with: title, product(s) to be opened, format, number of spots, price per spot, scheduled date and sale deadline. | Must | R1 |
| BRK-02 | A break follows a lifecycle: *Draft → Scheduled → On sale → Sold out → Live → Completed*, or *Cancelled*. | Must | R1 |
| BRK-03 | Supported formats: *Personal* (one buyer, whole product) and *Pick-your-spot* (buyer chooses a specific spot). | Must | R1 |
| BRK-04 | *Random spot* format (spots assigned randomly after sell-out) with an auditable, logged assignment. **Pending legal review (Q4).** | Could | R1 |
| BRK-05 | Breaks are visually and navigationally distinct from sealed products (own section, own product card, "Buy spot" call to action). | Must | R1 |
| BRK-06 | A spot can never be sold twice, even under concurrent purchases. | Must | R1 |
| BRK-07 | The break page shows remaining spots in near real time. | Should | R1 |
| BRK-08 | After the break, the Breaker records what was pulled for each spot; items go to the owner's vault. | Must | R1 |
| BRK-09 | Spot owners are notified of their results by email. | Must | R1 |
| BRK-10 | If a break does not sell out by its deadline, it can be cancelled and all spots refunded. | Must | R1 |
| BRK-11 | The site shows the Twitch live status and embeds the player when live. | Must | R1 |
| BRK-12 | Break schedule page, with "add to calendar" (.ics). | Should | R1 |
| BRK-13 | Customers can link their Twitch account so their Twitch name is shown on stream. | Should | R1 |
| BRK-14 | Past breaks page with VOD link and results. | Could | R2 |
| BRK-15 | Twitch chat bot announcing spot purchases. | Could | Later |

### 5.3 Vault and combined shipping (VLT)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| VLT-01 | Each customer has a vault listing items they own but have not received yet. | Must | R1 |
| VLT-02 | The customer selects vault items and requests a shipment, paying shipping at that moment. | Must | R1 |
| VLT-03 | At checkout, in-stock items can be marked "hold in vault" instead of "ship now", to combine with future break pulls. | Should | R1 |
| VLT-04 | Free storage period (configurable), with reminders before it ends and a defined policy afterwards. | Should | R1 |
| VLT-05 | Low-value pulls ("bulk") can be handled with a predefined option (ship, keep in vault, give back). | Could | R2 |

### 5.4 Cart and checkout (CHK)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| CHK-01 | The cart accepts any mix of product types and groups lines by fulfilment: *ships now*, *goes to vault* (break spots), *pre-order*. | Must | R1 |
| CHK-02 | Purchase limits per customer, per product or variant, enforced across orders (not only per cart) within a configurable period. | Must | R1 |
| CHK-03 | Stock and spots are reserved when checkout starts, with a timeout; reservations are released on timeout or failed payment. | Must | R1 |
| CHK-04 | Guest checkout for physical products; an account is required to buy break spots (the vault needs an owner). | Must | R1 |
| CHK-05 | The cart summary shows subtotal, VAT breakdown per rate, shipping and total. | Must | R1 |
| CHK-06 | Shipping cost depends on destination zone (Mainland, Azores, Madeira, EU…), parcel size/weight and carrier service. | Must | R1 |
| CHK-07 | Configurable free shipping threshold per zone. | Should | R1 |
| CHK-08 | Billing and shipping addresses; optional NIF / VAT number for the invoice. | Must | R1 |
| CHK-09 | Explicit acceptance of the terms and conditions, with information on the right of withdrawal. | Must | R1 |
| CHK-10 | Discount codes (percentage, fixed amount, free shipping) with validity dates and usage limits. | Should | R1 |
| CHK-11 | Delivery to pickup points / lockers. | Could | R2 |

### 5.5 Payments (PAY)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| PAY-01 | Payment via Easypay: MB WAY, Multibanco reference and card (with 3-D Secure). | Must | R1 |
| PAY-02 | Payment confirmation is received via webhook; processing is idempotent (the same notification twice has no extra effect). | Must | R1 |
| PAY-03 | Expired Multibanco references / MB WAY requests cancel the order and release reserved stock. | Must | R1 |
| PAY-04 | Full and partial refunds from the back office. | Must | R1 |
| PAY-05 | Apple Pay, Google Pay, PayPal. | Could | R2 |

### 5.6 Invoicing and tax (TAX)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| TAX-01 | An invoice-receipt is issued automatically through InvoiceXpress when payment is confirmed; the PDF is emailed and available in the customer account. | Must | R1 |
| TAX-02 | Refunds issue a credit note. | Must | R1 |
| TAX-03 | The VAT rate is determined by configurable rules (seller VAT regime, ship-from location, destination region, product tax category) — no hard-coded rates. **See Q1–Q3.** | Must | R1 |
| TAX-04 | Support for VAT exemption (article 53 of CIVA), with the legally required mention on invoices. | Must | R1 |
| TAX-05 | Support for the margin scheme for second-hand goods (e.g. singles bought from private sellers). **See Q3.** | Could | R2 |

### 5.7 Shipping and fulfilment (SHP)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| SHP-01 | Carrier integration: create shipment, print label, obtain tracking number. One carrier in R1. | Must | R1 |
| SHP-02 | Fulfilment workflow: *To pack → Packed → Shipped → Delivered*, with a pick list. | Must | R1 |
| SHP-03 | Tracking information is emailed and shown in the customer account. | Must | R1 |
| SHP-04 | Stock is tracked per location (e.g. Terceira warehouse, other locations in the future). | Should | R1 |
| SHP-05 | Insured / signature-required shipping for high-value orders. | Should | R1 |
| SHP-06 | Shipping to EU countries. | Should | R1 |
| SHP-07 | Shipping outside the EU, with customs documents. | Could | Later |
| SHP-08 | Additional carriers. | Could | R2 |

### 5.8 Auctions (AUC)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| AUC-01 | Timed online auctions: starting price, bid increment, optional reserve price, end date. | Could | R2 |
| AUC-02 | Anti-sniping: a bid in the last minutes extends the end time. | Could | R2 |
| AUC-03 | The winner must pay within a deadline; otherwise the item is offered to the next bidder or relisted. | Could | R2 |
| AUC-04 | Live auctions during the Twitch stream. | Could | Later |

### 5.9 Customer account (ACC)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| ACC-01 | Registration and login with email and password; email verification; password reset. | Must | R1 |
| ACC-02 | Social login (Google, Twitch). | Should | R1 |
| ACC-03 | Order history with invoices and tracking. | Must | R1 |
| ACC-04 | Vault view (see VLT). | Must | R1 |
| ACC-05 | Address book. | Must | R1 |
| ACC-06 | Language preference (PT/EN) used for site and emails. | Must | R1 |
| ACC-07 | GDPR self-service: data export, account deletion, consent management. | Must | R1 |

### 5.10 Back office (ADM)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| ADM-01 | Role-based access: Admin, Staff, Breaker. | Must | R1 |
| ADM-02 | Product management: types, variants, drag-and-drop images, categories, attributes, price, stock, purchase limits, SEO fields, PT and EN content side by side. | Must | R1 |
| ADM-03 | Order management: search, filters, status changes, internal notes, refunds. | Must | R1 |
| ADM-04 | Fulfilment screen optimised for minimal clicks: open order, print label, mark as shipped. | Must | R1 |
| ADM-05 | Break management: create, monitor spot sales, record results per spot quickly during or after the stream. | Must | R1 |
| ADM-06 | Customer management: profile, orders, vault, purchase-limit history. | Must | R1 |
| ADM-07 | Homepage and menu editor. | Must | R1 |
| ADM-08 | Category and attribute management. | Must | R1 |
| ADM-09 | Dashboard: sales, orders to ship, low stock, upcoming breaks. | Should | R1 |
| ADM-10 | Bulk import/export of products (CSV). | Should | R1 |
| ADM-11 | Email template editing (PT/EN). | Should | R1 |
| ADM-12 | Audit log of back-office actions (who changed what, when). | Should | R1 |
| ADM-13 | Stock sync with Cardmarket (avoid selling the same single twice). **See Q8.** | Could | R2 |

### 5.11 Notifications (NTF)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| NTF-01 | Transactional emails in the customer's language: account verification, password reset, order confirmation, Multibanco payment details, payment received, invoice, shipped (with tracking), break reminder, break results, vault expiry reminder, refund. | Must | R1 |
| NTF-02 | Newsletter subscription with separate, logged consent. | Could | R2 |

### 5.12 Legal and compliance (LEG)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| LEG-01 | Pages: Terms and Conditions, Privacy Policy, Cookie Policy, Returns and Withdrawal, Shipping, Break Rules. | Must | R1 |
| LEG-02 | Visible link to the *Livro de Reclamações Eletrónico*. | Must | R1 |
| LEG-03 | Information on Alternative Dispute Resolution entities (RAL). | Must | R1 |
| LEG-04 | Seller identification: name, NIF, address, contacts. | Must | R1 |
| LEG-05 | Cookie consent banner; no non-essential cookies before consent. | Must | R1 |
| LEG-06 | Marketing consent separate from order acceptance, and logged. | Must | R1 |
| LEG-07 | Minimum age confirmation for break spots. **See Q9.** | Should | R1 |

### 5.13 Internationalisation (I18N)

| ID | Requirement | Priority | Release |
|---|---|---|---|
| I18N-01 | The whole site is available in Portuguese (pt-PT, default) and English (en). | Must | R1 |
| I18N-02 | Localised URLs (`/pt/...`, `/en/...`) with `hreflang` tags. | Must | R1 |
| I18N-03 | Product and CMS content is translatable; a missing translation falls back to the other language. | Must | R1 |
| I18N-04 | Dates, numbers and currency are formatted per locale. | Must | R1 |
| I18N-05 | New languages can be added by providing translations only, without code changes. | Should | R1 |
| I18N-06 | Multi-currency. | Won't | — |

## 6. Non-functional requirements

Targets marked with † are initial estimates to be validated once real traffic data exists.

### 6.1 Performance and scalability

| ID | Requirement |
|---|---|
| NFR-PERF-01 | Core Web Vitals on mobile (p75): LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1. |
| NFR-PERF-02 | Catalogue API responses p95 < 300 ms. |
| NFR-SCAL-01 | During a live break the system handles 500 concurrent users and 50 purchase attempts per second on the same break without errors.† |

### 6.2 Data consistency

| ID | Requirement |
|---|---|
| NFR-CONS-01 | Stock and spot allocation are strongly consistent: overselling is impossible, verified by automated concurrency tests. |
| NFR-CONS-02 | Monetary values are stored as integer cents with a currency code; rounding rules are defined once and match the invoices. |

### 6.3 Availability and recovery

| ID | Requirement |
|---|---|
| NFR-AVAIL-01 | 99.5 % monthly availability; planned maintenance never overlaps scheduled breaks. |
| NFR-BKP-01 | Daily database backups kept for 30 days; restore procedure tested. RPO 24 h, RTO 4 h.† |

### 6.4 Security

| ID | Requirement |
|---|---|
| NFR-SEC-01 | Protection against the OWASP Top 10. |
| NFR-SEC-02 | Passwords hashed with a modern algorithm (Argon2id or bcrypt); two-factor authentication for back-office users. |
| NFR-SEC-03 | Card data never reaches our servers (hosted payment page/fields — PCI DSS SAQ A). |
| NFR-SEC-04 | Webhooks are authenticated (signature or equivalent) and processed idempotently. |
| NFR-SEC-05 | Rate limiting on login, registration, checkout and bidding. |
| NFR-SEC-06 | Secrets are kept in environment variables / a secret manager, never in the repository. |
| NFR-SEC-07 | Back-office access is role-based and every sensitive action is logged. |

### 6.5 Privacy (GDPR)

| ID | Requirement |
|---|---|
| NFR-PRIV-01 | Data minimisation: only data needed for the stated purposes is collected. |
| NFR-PRIV-02 | Defined retention periods per data category (e.g. invoices are kept as long as tax law requires). |
| NFR-PRIV-03 | Personal data hosted in the EU; data processing agreements with all processors. |

### 6.6 Usability and accessibility

| ID | Requirement |
|---|---|
| NFR-USE-01 | Mobile-first design — most Twitch viewers browse on phones. |
| NFR-USE-02 | A non-technical person completes the core back-office tasks (add product, ship order, record break results) without training, validated by a usability test. |
| NFR-USE-03 | Destructive back-office actions require confirmation or can be undone. |
| NFR-A11Y-01 | WCAG 2.2 level AA. |
| NFR-COMP-01 | Supports the last two versions of Chrome, Safari, Firefox and Edge, on desktop and mobile. |

### 6.7 SEO

| ID | Requirement |
|---|---|
| NFR-SEO-01 | Public pages are server-rendered with unique titles and meta descriptions. |
| NFR-SEO-02 | Structured data (schema.org `Product`, `Offer`, `BreadcrumbList`), XML sitemap, canonical URLs, `hreflang`. |

### 6.8 Maintainability and quality

| ID | Requirement |
|---|---|
| NFR-MAINT-01 | Code, comments, commits and technical documentation in English. |
| NFR-MAINT-02 | Static typing in strict mode, linting and formatting enforced in CI. |
| NFR-MAINT-03 | Conventional Commits; every change goes through a pull request with passing CI. |
| NFR-MAINT-04 | External providers (payments, carrier, invoicing, email) sit behind internal interfaces so they can be replaced without touching business logic. |
| NFR-TEST-01 | Unit tests for domain logic (≥ 80 % coverage); integration tests for database and providers; end-to-end tests for critical flows (checkout, payment webhook, spot purchase). |
| NFR-OBS-01 | Structured logs, error tracking, uptime monitoring and alerts. |
| NFR-PORT-01 | Local development environment reproducible with Docker. |
| NFR-DOC-01 | Significant technical decisions are recorded as ADRs. |

## 7. Constraints and assumptions

- The seller is currently a sole trader (*trabalhador independente*) in Portugal; the VAT regime is to be confirmed.
- Payments: Easypay. Invoicing: InvoiceXpress. Both chosen for existing team experience.
- Main stock location: Terceira, Azores.
- No WordPress, Shopify or other off-the-shelf store platform — custom code.
- Low running costs at launch.

## 8. Open questions

| # | Question | Who answers |
|---|---|---|
| Q1 | Which VAT regime applies at launch: exemption under article 53 of CIVA, or the normal regime? This changes prices, invoices and the "VAT included" legend. | Accountant |
| Q2 | Which VAT rate applies to goods shipped from the Azores warehouse to customers on the Mainland, Madeira and the rest of the EU? | Accountant |
| Q3 | Should singles bought from private sellers use the margin scheme for second-hand goods? | Accountant |
| Q4 | Are *random spot* breaks allowed under Portuguese gaming law (SRIJ), given that buyers pay for a random outcome? Are *pick-your-spot* breaks safe? | Lawyer |
| Q5 | Imports from the US: commercial goods are normally subject to customs duties and import VAT regardless of the importer's nationality. What actually applies to our case? | Customs broker / accountant |
| Q6 | Which carrier(s) serve Terceira with an API (CTT, DPD, GLS, an aggregator)? Costs per zone? | Team |
| Q7 | Will there be a second stock location (e.g. Mainland)? | Team |
| Q8 | Must stock be synchronised with Cardmarket from day one? | Team |
| Q9 | Minimum age to buy break spots? | Lawyer / Team |
| Q10 | Vault: free storage period, and what happens after it ends? | Team |
| Q11 | Which break formats do you run today, and how are spots priced? | Team |
| Q12 | Auctions: timed online, live on stream, or both? | Team |

## 9. Out of scope (for now)

NFTs, real-world asset tokenisation, crypto payments and a digital TCG. The architecture will not prevent them, but no work is planned until there is a business case.
