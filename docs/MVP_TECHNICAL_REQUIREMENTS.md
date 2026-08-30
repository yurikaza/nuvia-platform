# MVP Technical Requirements

> **The first objective is to validate the business model — not to build a large platform.** The MVP exists to make the weekly loop run for 50–100 customers with one operations coordinator in the middle.

## 1. Engineering Principles

**Do not over-engineer.** This is a hard constraint.

| Principle | What it means here |
|---|---|
| **One application, four surfaces** | A single web codebase with role-based access: customer, dietitian, operations, courier. |
| **Customer app is core** | The customer-facing product is not optional. It owns the customer relationship, plan visibility, basket approval, delivery state, and payment experience. |
| **Dietitian software is a free professional tool** | The dashboard is a core acquisition/retention product for dietitians, not a paid SaaS add-on in Phase 1. |
| **Manual is a feature** | Suppliers and some courier operations can use WhatsApp while volume is low. |
| **Web first** | Responsive web/PWA for all four surfaces. Native mobile apps are not required in Phase 1. |
| **Turkish first** | Turkish UI, phone/address conventions, TL and Turkish payment rails. |
| **Build for 100 customers** | Do not solve scaling problems before the pilot creates them. |
| **Instrument the metrics** | Retention, repeat orders, delivery economics, complaints and partner activation must be queryable from day one. |

**Build budget:** approximately 2 weeks after discovery. Anything that does not help prove the pilot hypothesis is deferred.

## 2. Architecture Overview

```text
┌────────────────────────────────────────────────────────────────────┐
│                         ONE WEB APPLICATION                         │
├────────────────┬────────────────┬─────────────────┬─────────────────┤
│    CUSTOMER    │   DIETITIAN    │   OPERATIONS    │     COURIER     │
│ mobile-first   │ desktop-first  │ internal        │ mobile-first    │
│ core product   │ free tool      │ control plane   │ route + SoftPOS │
└────────────────┴────────────────┴─────────────────┴─────────────────┘
                                  │
                          ┌───────▼────────┐
                          │    BACKEND     │
                          │ users • plans  │
                          │ baskets • orders│
                          │ payments       │
                          │ deliveries     │
                          └───────┬────────┘
                                  │
             ┌────────────────────┼─────────────────────┐
             ▼                    ▼                     ▼
        PostgreSQL          Payment provider       SMS / Maps
```

A single application is appropriate because all surfaces share customers, plans, orders, payments and delivery state.

## 3. Recommended Stack

| Layer | Recommendation |
|---|---|
| Framework | Next.js App Router |
| Language | TypeScript |
| UI | Tailwind CSS + shadcn/ui |
| Database | PostgreSQL |
| ORM | Drizzle or Prisma — choose the familiar one |
| Auth | Phone/SMS OTP for customers/couriers; email/password for professionals/ops |
| Payment | Turkish PSP with SoftPOS/mobile acceptance and a settlement API suitable for Nuvia's model; provider capability must be validated before implementation |
| SMS | Local Turkish SMS provider |
| Maps | Google Maps Platform |
| Hosting | Vercel |
| File storage | Vercel Blob or equivalent for delivery evidence |
| Error tracking | Sentry |
| Analytics | Postgres queries + internal metrics page |

Native apps, microservices, queues, Kubernetes, GraphQL, a separate route-optimisation service and a data warehouse are out of scope.

## 4. Backend Scope

### 4.1 User Management

- Roles: `customer`, `dietitian`, `operations`, `courier`, `supplier`.
- Customer onboarding primarily via dietitian/gym invitation.
- Role-based access enforced server-side.
- Dietitian sees only their clients.
- Courier sees only assigned deliveries, delivery notes and the minimum customer data required for the route.
- Supplier access may remain ops-managed in Phase 1 rather than requiring a supplier portal.

### 4.2 Nutrition Plans

- Dietitian-owned plan templates.
- Days → meals → food items → quantities/units.
- Per-customer constraints: allergies, dislikes, household size, budget band.
- Plan versioning.
- Mapping from plan food to purchasable supplier products.
- The nutrition decision remains with the dietitian; Nuvia handles execution and logistics.

### 4.3 Basket Generation

- Weekly basket generated from the active plan.
- Purchase-unit rounding without dropping below the plan requirement.
- Unmatched product flagging for manual resolution.
- Dietitian reviews and confirms the basket.
- Customer sees the generated basket and can approve, skip, or select a dietitian-approved alternative.
- The basket is intentionally **not** a general grocery marketplace.

### 4.4 Orders

Phase 1 order states:

```text
generated
→ dietitian_confirmed
→ customer_approved
→ preparing
→ out_for_delivery
→ delivered
→ paid
→ settled
```

Operational/payment exception states:

```text
skipped
cancelled
payment_failed
payment_refused
delivery_failed
partially_refunded
fully_refunded
manual_review
```

The important distinction is that **customer approval and customer payment are separate states**. Approval commits the order to the route; payment occurs at delivery via courier SoftPOS.

### 4.5 Subscriptions

- Weekly recurring plan.
- Customer can pause, skip one week, resume and cancel.
- Subscription generates the next basket automatically.
- No automatic customer charge before delivery in Phase 1.
- Capture cancellation reason.

### 4.6 Payments

**Confirmed Phase 1 UX:**

```text
Customer approves basket
        ↓
No payment yet
        ↓
Supplier prepares order
        ↓
Courier picks up order
        ↓
Courier arrives
        ↓
Customer sees package
        ↓
Courier accepts card payment via SoftPOS
        ↓
Payment succeeds
        ↓
Delivery/payment recorded
        ↓
Settlement process begins
```

Requirements:

- Courier-side SoftPOS payment initiation.
- Payment result tied to the exact order ID.
- Customer sees the amount due in the app.
- No card data stored by Nuvia.
- Payment receipt/reference stored.
- Payment failure state and controlled retry flow.
- Settlement ledger for supplier(s), courier, dietitian and Nuvia shares.
- No Nuvia-built wallet or escrow mechanism.
- Exact acquiring/settlement architecture must be confirmed with an authorised Turkish payment provider before production.

### 4.7 Dietitian Dashboard

This is a **P0 product**, not an administrative afterthought.

- Client management.
- Plan creation and templates.
- Weekly basket review.
- Client adherence signals.
- Retention view.
- Order history.
- Commission ledger.
- Client invitation flow.

The dashboard is free for active partners in Phase 1. The commercial incentive is primarily client retention and professional tooling; approximately 5% commission on completed orders is secondary.

### 4.8 Customer Application

The customer application is the primary consumer product.

P0:

- Registration/login.
- Dietitian connection.
- Profile and delivery address with mandatory map pin.
- Current nutrition plan viewing.
- Weekly basket view with itemised prices.
- Basket approval / skip.
- Delivery window.
- Order status.
- Payment-due-at-delivery status.
- Delivery tracking on delivery day.
- Subscription pause/skip/resume/cancel.
- Payment/SoftPOS receipt history.
- Direct support entry.

P1:

- Weight/progress tracking visible to the dietitian.
- Adherence streak.

The app should make Nuvia feel like the customer's **lifestyle system**, not like a grocery store.

### 4.9 Delivery & Routing

- Delivery-day scheduling.
- Geographic clustering.
- Manual route assembly with a simple distance heuristic.
- Courier assignment.
- Route publication before the shift.
- Supplier pickup checklist.
- Stop confirmation.
- Delivery exception codes.
- SoftPOS transaction confirmation at the stop.

The courier must see the route, time windows and expected route pay before starting.

### 4.10 Notifications

| Trigger | Channel | Recipient |
|---|---|---|
| Basket ready | SMS + in-app | Customer |
| Approval cutoff reminder | SMS + in-app | Customer |
| Order accepted | In-app | Customer |
| Courier en route | SMS + in-app | Customer |
| Payment completed | In-app + receipt | Customer |
| Route published | SMS/in-app | Courier |
| Client action required | Email/in-app | Dietitian |
| Weekly summary | Email/in-app | Dietitian |

## 5. Data Model

| Entity | Key fields |
|---|---|
| `user` | id, role, phone, email, name, created_at, status |
| `customer_profile` | user_id, address, geo point, delivery notes, preferred window, allergies, dislikes, household size, dietitian_id, acquisition channel |
| `dietitian_profile` | user_id, clinic, commission rate, status, signed_at |
| `courier_profile` | user_id, vehicle, availability, status |
| `supplier` | id, name, category, contact, pickup window, settlement terms, status |
| `product` | id, supplier_id, name, unit, purchase-unit size, price, spec notes |
| `plan_template` | id, dietitian_id, name, structure |
| `plan` | id, customer_id, dietitian_id, template_id, version, active_from |
| `plan_item` | plan_id, day, meal, food, quantity, unit, product_id |
| `order` | id, customer_id, week, state, total, approved_at, delivery_at |
| `order_item` | order_id, product_id, quantity, unit_price, line_total, substituted_from |
| `subscription` | customer_id, state, paused_until, cancelled_at, cancellation_reason |
| `payment` | order_id, method, state, PSP reference, amount, receipt reference |
| `settlement` | order_id, beneficiary_type, beneficiary_id, amount, state, released_at, provider_reference |
| `commission` | dietitian_id, order_id, amount, settlement_id |
| `route` | id, delivery_date, courier_id, state, stop_count, courier_payment |
| `delivery` | route_id, order_id, sequence, window, state, delivered_at, payment_confirmed_at, failure_reason |
| `complaint` | order_id, product_id, supplier_id, type, description, resolution, resolved_at |
| `progress_entry` | customer_id, date, weight, optional measurements |

## 6. Build Order

1. Auth, roles and user records.
2. Dietitian dashboard: clients and plan creation.
3. Customer onboarding, profile and plan viewing.
4. Product catalogue and pricing.
5. Basket generation from real dietitian plans.
6. Customer basket approval and skip flow.
7. Operations order board.
8. Delivery assignment and route view.
9. Courier mobile interface.
10. SoftPOS/payment integration.
11. Settlement/reconciliation ledger.
12. Notifications and support.
13. Metrics/cohort page.
14. P1 progress tracking.

The payment integration should be implemented only after provider validation. Do not code against an assumed settlement API.

## 7. Phase 1 Shortcuts

- WhatsApp supplier pick lists.
- Manual supplier price updates.
- Manual route sequencing.
- Manual courier payout reconciliation if the provider cannot automate it.
- Manual dietitian commission payout reporting.
- No inventory system because Nuvia does not hold inventory.
- No native mobile apps.
- No public product marketplace.

## 8. Non-Functional Requirements

| Area | Requirement |
|---|---|
| Performance | Customer basket approval should feel fast on 4G. |
| Mobile | Customer and courier interfaces mobile-first. Courier UI usable one-handed. |
| Security | Server-side authorisation; no card data stored by Nuvia; least-privilege partner access; audit trail for order/payment/settlement state changes. |
| Privacy | KVKK requirements confirmed with local advisor; minimum necessary personal data. |
| Reliability | Avoid deployments around the weekly operational window. |
| Offline tolerance | Courier app should tolerate brief connectivity loss and safely retry delivery/payment callbacks. |
| Observability | Structured logs for order, payment, delivery and settlement transitions. |

## 9. Out of Scope for Phase 1

Native mobile apps, recipes, macro/calorie logging, food photo diaries, social/community features, gamification, in-app dietitian chat, public marketplace browsing, customer-created baskets, multi-city support, automated route optimisation, ML recommendations, microservices, GraphQL, data warehouse, Kubernetes and third-party integrations beyond the validated payment/SMS/maps stack.

**Customer application and dietitian dashboard are explicitly NOT out of scope. They are core Phase 1 surfaces.**
