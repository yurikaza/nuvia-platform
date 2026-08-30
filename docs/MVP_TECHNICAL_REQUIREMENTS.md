# MVP Technical Requirements

> **The first objective is to validate the business model — not to build a platform.**
>
> Every hour spent on architecture is an hour not spent talking to dietitians. The MVP exists to make the weekly loop run for 50–100 customers with one operations coordinator in the middle. Nothing more.

---

## 1. Engineering Principles

**Do not over-engineer.** This is a hard constraint, not a preference.

| Principle | What it means here |
|---|---|
| **One application, four surfaces** | A single codebase with role-based access. Not microservices, not four apps, not a monorepo of packages. |
| **Boring, proven stack** | Nothing chosen for interest. Every technology should be one the team can debug at 22:00 on a Saturday. |
| **Manual is a feature** | If a human can do it in 10 minutes a week, do not automate it in Phase 1. Manual steps reveal the real process. |
| **Web everywhere** | Responsive web for all four surfaces. No native apps. Couriers use mobile web. |
| **Turkish first** | Turkish UI, Turkish phone formats, Turkish addressing, Turkish payment rails, TL. |
| **Build for 100 customers** | Not 10,000. Scaling problems we do not have are the cheapest problems to ignore. |
| **Instrument the metrics** | The metrics in [`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) §8 must be queryable from day one. This is the one place to be rigorous — the pilot's entire output is data. |

**The build budget is 2 weeks** (weeks 3–4 of [`VALIDATION_PLAN.md`](./VALIDATION_PLAN.md)). Any requirement that does not fit is deferred, not compressed.

---

## 2. Architecture Overview

```
┌──────────────────────────────────────────────────────────────┐
│                    ONE WEB APPLICATION                       │
│                  (role-based routing/access)                 │
├──────────────┬──────────────┬──────────────┬─────────────────┤
│  CUSTOMER    │  DIETITIAN   │  OPERATIONS  │    COURIER      │
│  responsive  │  desktop-    │  desktop     │  mobile web     │
│  mobile web  │  first       │  internal    │  (one-hand use) │
└──────────────┴──────────────┴──────────────┴─────────────────┘
                              │
                    ┌─────────▼─────────┐
                    │     BACKEND       │
                    │  users • orders   │
                    │  subscriptions    │
                    │  payments         │
                    │  partners         │
                    └─────────┬─────────┘
                              │
        ┌──────────┬──────────┼──────────┬──────────┐
        ▼          ▼          ▼          ▼          ▼
   ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐
   │Postgres│ │  PSP   │ │  SMS   │ │  Maps  │ │ Object │
   │        │ │(iyzico/│ │        │ │        │ │ store  │
   │        │ │ PayTR) │ │        │ │        │ │(photos)│
   └────────┘ └────────┘ └────────┘ └────────┘ └────────┘
```

**Why a single application:** four surfaces share the same core entities (customers, plans, orders, deliveries). Splitting them means synchronising state across services for zero benefit at this scale.

---

## 3. Recommended Stack

Chosen for delivery speed and operability by a very small team. Any equivalent the team already knows well is a valid substitute — **familiarity beats optimality here**.

| Layer | Recommendation | Why |
|---|---|---|
| Framework | **Next.js (App Router)** | One codebase for UI and API; server components reduce client complexity; fast to ship |
| Language | **TypeScript** | Shared types between surfaces prevents a whole class of bug at zero cost |
| UI | **Tailwind CSS + shadcn/ui** | Four surfaces at speed without designing a system |
| Database | **PostgreSQL** (Neon via Vercel Marketplace) | Relational data, relational model. Nothing here wants a document store. |
| ORM | **Drizzle** or **Prisma** | Either is fine; pick the one the team knows |
| Auth | **Phone + SMS OTP** for customers and couriers; **email + password** for dietitians and ops | Turkish customers expect phone auth; couriers will not manage passwords |
| Payments | **iyzico** or **PayTR** | Turkish PSPs with card storage and recurring support. Validate rates and settlement terms before choosing. |
| SMS | Local Turkish SMS provider | Notification backbone; more reliable than push in Phase 1 |
| Maps | **Google Maps Platform** | Best Turkish address and geocoding coverage; needed for pins and route links |
| Hosting | **Vercel** | Deploy speed; no infrastructure work |
| File storage | **Vercel Blob** | Delivery photos only |
| Error tracking | **Sentry** | |
| Analytics | Postgres queries + a simple ops metrics page | Do not add an analytics platform for 100 customers |

**Deliberately excluded from Phase 1:** native mobile apps, real-time infrastructure (WebSockets), a message queue, a separate route-optimisation service, a data warehouse, Kubernetes or containers, microservices, GraphQL, a design system, i18n framework (Turkish only), and a CMS.

---

## 4. Backend Scope

### 4.1 User Management
- Four roles: `customer`, `dietitian`, `operations`, `courier`
- Registration via invite code (customers) or ops-created account (dietitian, courier, ops)
- Phone/SMS OTP and email/password authentication
- Role-based access enforced server-side on every request
- Profile management per role
- **Access boundaries:** a dietitian sees only their own clients; a courier sees only today's assigned stops with masked phone numbers; ops sees everything; a customer sees only themselves

### 4.2 Nutrition Plans
- Plan templates owned by a dietitian, cloneable per client
- Plan structure: days → meals → items with quantities
- Item catalogue mapping plan foods to purchasable supplier products with purchase units
- Per-client constraints: allergies, dislikes, household size, budget band
- Plan versioning — enough to know which plan produced which basket

### 4.3 Orders
- Weekly basket generation from a plan (scheduled job, Thursday 09:00)
- Purchase-unit rounding, never below plan requirement
- Unmatched-item flagging for manual resolution
- Dietitian review and confirmation
- Customer approval, swap within allowed alternatives, or skip
- Hard cutoff enforcement (Friday 18:00)
- Order states: `generated → dietitian_confirmed → customer_approved → paid → preparing → out_for_delivery → delivered` (plus `skipped`, `cancelled`, `failed`)
- Per-supplier pick-list aggregation across all approved orders

### 4.4 Subscriptions
- Weekly recurrence as the default state
- Pause, skip a single week, resume, cancel — all self-service
- Delivery window and address preferences
- Cancellation reason capture (**required** — this is a primary pilot output)

### 4.5 Payments
- Card charge on approval, via PSP hosted flow (no card data touches our systems)
- Saved card token for recurring weeks
- Cash-on-delivery flag with courier-side collection recording
- Retry on failure, then notify, then remove from route
- Refunds, partial refunds, and goodwill credits
- Dietitian commission accrual on delivery confirmation, monthly payout report
- Reconciliation view: orders vs charges vs settlements

### 4.6 Partner Management
- Dietitians: profile, clients, commission rate, order history, payouts
- Suppliers: contact, product catalogue with prices, pickup times, quality complaint log
- Couriers: profile, availability, assigned routes, payment records, performance
- Fitness centres: referral tracking, revenue share basis

### 4.7 Delivery & Routing
- Delivery-day scheduling
- Geographic clustering of approved orders
- Manual route assembly with a nearest-neighbour ordering assist
- Courier assignment and route publication (Saturday 10:00)
- Stop-level delivery confirmation, photo upload, failure reason codes
- Cash collection recording and end-of-day reconciliation

### 4.8 Notifications
| Trigger | Channel | Recipient |
|---|---|---|
| Basket ready for approval | SMS | Customer |
| Approval cutoff reminder | SMS | Customer |
| Payment failed | SMS | Customer |
| Out for delivery | SMS | Customer |
| Delivered | SMS | Customer |
| Route published | SMS | Courier |
| Clients awaiting basket confirmation | Email | Dietitian |
| Weekly summary | Email | Dietitian |

### 4.9 Metrics
Every Tier 1 and Tier 2 metric from [`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) §8, queryable and shown on a single ops metrics page. Cohort retention by signup week and by acquiring dietitian is **required**, not optional — the pilot's conclusions depend on it.

---

## 5. Data Model (Entities)

Described as entities and key fields, not as schema. Implementation detail belongs in the codebase, not here.

| Entity | Key fields |
|---|---|
| `user` | id, role, phone, email, name, created_at, status |
| `customer_profile` | user_id, address, geo point, delivery notes, preferred window, allergies, dislikes, household size, dietitian_id, acquisition channel |
| `dietitian_profile` | user_id, clinic, commission rate, status, signed_at |
| `courier_profile` | user_id, vehicle type, availability, status |
| `supplier` | id, name, category, contact, pickup window, status |
| `product` | id, supplier_id, name, unit, purchase unit size, price, spec notes |
| `plan_template` | id, dietitian_id, name, structure |
| `plan` | id, customer_id, dietitian_id, template_id, version, active_from |
| `plan_item` | plan_id, day, meal, food, quantity, unit, product_id |
| `order` | id, customer_id, week, state, total, approved_at, cutoff_at, skip_reason |
| `order_item` | order_id, product_id, quantity, unit price, line total, substituted_from |
| `subscription` | customer_id, state, paused_until, cancelled_at, cancellation_reason |
| `payment` | order_id, method, state, psp_reference, amount, refunded_amount |
| `commission` | dietitian_id, order_id, amount, payout_id |
| `route` | id, delivery_date, courier_id, state, stop count, courier_payment |
| `delivery` | route_id, order_id, sequence, window, state, delivered_at, photo_url, failure_reason |
| `complaint` | order_id, product_id, supplier_id, type, description, resolution, resolved_at |
| `progress_entry` | customer_id, date, weight, measurements |

---

## 6. Build Order

Sequenced so the loop can be tested manually before it is complete. **Nothing here is worth building out of order.**

| # | Deliverable | Why first |
|---|---|---|
| 1 | Auth, roles, user records | Everything depends on it |
| 2 | Ops dashboard: customer, supplier, courier records | Ops can run the business by hand from here |
| 3 | Product catalogue and pricing | Baskets cannot be priced without it |
| 4 | Dietitian: clients, plan templates, plan creation | The demand source |
| 5 | Basket generation from plan | The core mechanic — build and test with real plans |
| 6 | Customer: registration, profile, basket approval | Closes the demand loop |
| 7 | Payment integration | Real money, real signal |
| 8 | Supplier pick-list aggregation | Removes the largest manual ops burden |
| 9 | Route building and courier assignment | |
| 10 | Courier interface | Last, because ops can dispatch by WhatsApp until it exists |
| 11 | Notifications | |
| 12 | Metrics page and cohort queries | Must exist before the first customer is served |
| 13 | Progress tracking | P1 — ship if time allows |

**If the two-week budget runs out at step 9,** the pilot can still run: dispatch couriers by WhatsApp with a printed route. It cannot run without steps 1–8.

---

## 7. Acceptable Shortcuts

Explicitly sanctioned for Phase 1. Each is a conscious trade, not an accident.

| Shortcut | Rationale | Revisit at |
|---|---|---|
| WhatsApp for supplier pick lists | Suppliers will not log into a portal | Phase 2 |
| WhatsApp deeplink for customer support | Faster than building a ticketing system | 250+ customers |
| Manual route sequencing | Optimisation is not the bottleneck at 10–20 stops | Phase 2 |
| Manual courier payouts | 3 couriers, weekly | 10+ couriers |
| Manual commission payouts | 10 dietitians, monthly | 30+ dietitians |
| Spreadsheet supplier catalogue import | The catalogue is small and changes rarely | Phase 2 |
| No inventory tracking | We hold no inventory in Phase 1 | Phase 2 (mandatory) |
| SMS instead of push | No app; SMS is more reliable in this market | When a native app exists |
| Single delivery day hard-coded | It genuinely is single | Second delivery day |
| Ops metrics page over an analytics platform | 100 customers | Phase 2 |

---

## 8. Non-Functional Requirements

| Area | Requirement |
|---|---|
| Performance | Page load under 2s on 4G. Customers approve baskets on phones, often outdoors. |
| Availability | Best-effort. A few minutes of downtime on a Tuesday costs nothing; downtime Thursday–Sunday costs a week. Avoid deploys Thursday 08:00 → Sunday 18:00. |
| Mobile | Customer and courier surfaces are mobile-first. The courier interface must be usable one-handed. |
| Offline | Courier interface should tolerate brief connectivity loss and queue delivery confirmations. |
| Security | Server-side authorisation on every request; no card data stored; masked phone numbers for couriers; audit trail on order and payment state changes |
| Privacy | KVKK-compliant consent at signup; minimum necessary data; documented retention policy (see [`RISKS_AND_MITIGATION.md`](./RISKS_AND_MITIGATION.md) Risk 12) |
| Backups | Daily automated Postgres backups; verify a restore once before launch |
| Observability | Sentry for errors; structured logs on order state transitions and payment events |

---

## 9. Out of Scope for Phase 1

Recorded so they are not re-litigated mid-build:

**Product:** native apps, recipes and cooking instructions, calorie/macro logging, photo food diaries, in-app dietitian chat, social or community features, gamification, referral programs, multiple addresses, gift subscriptions, a public marketplace, customer-driven product browsing.

**Technical:** microservices, GraphQL, real-time infrastructure, message queues, automated route optimisation, ML/recommendation systems, a data warehouse, multi-tenancy, multi-city support, i18n beyond Turkish, a public API, third-party integrations beyond PSP/SMS/maps, mobile push, A/B testing infrastructure.

**Rule:** anything on this list needs a written justification tied to a Phase 1 success metric before it is reconsidered.
