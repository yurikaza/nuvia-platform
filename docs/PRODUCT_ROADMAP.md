# Product Roadmap

Three operating phases, each with one question to answer. A phase does not start until the previous phase's question is answered with evidence.

| Phase | Horizon | Question | Model |
|---|---|---|---|
| **1 — Atakum Pilot** | Months 0–6 | Will customers repeatedly buy plan-linked baskets, and will professional partners keep using Nuvia? | Local suppliers + planned courier network |
| **2 — Micro Fulfilment** | Months 6–18 | Can we control cost and quality at volume? | Centralised inventory + fulfilment |
| **3 — Nutrition Production** | Months 18–36 | Will customers buy prepared personalised meals? | Nutrition production company |
| **4 — Network Expansion** | Months 36+ | Can the operating playbook transfer to new districts/cities? | Local network replication |

---

# Phase 1: Atakum Pilot

## Goal

Validate the complete weekly loop:

```text
Dietitian plan
→ basket
→ customer approval
→ supplier preparation
→ planned pickup
→ courier delivery
→ SoftPOS payment at the door
→ supplier/courier/dietitian settlement
→ reorder
```

Phase 1 is not about maximum profit. It is about proving that the loop creates repeat behaviour and that every participant has a reason to stay.

## Targets

| Target | Number |
|---|---:|
| Dietitian partners | 10 signed; 5+ actively generating orders |
| Fitness centre partners | 2–3 |
| Active customers | 50–100 |
| Couriers | 2–3 |
| Suppliers | 2–4 |
| Districts | Atakum only |

## Success Criteria

- ≥40% of week-1 customers complete week 4.
- ≥5 dietitians actively generate orders in the final month without repeated prompting.
- Contribution margin per delivery ≥0 at ≥60 active customers.
- Quality complaint rate <5% of deliveries.
- Customer sentiment is positive in structured week-8 interviews.
- Supplier partners accept the short settlement model and continue releasing approved orders.
- Customers demonstrate acceptance of **payment at delivery via SoftPOS**.

---

# Phase 1 Product Surfaces

Nuvia has four product surfaces. Two are customer-facing/professional products and two are operational.

```text
                         NUVIA
                           │
          ┌────────────────┼────────────────┐
          │                │                │
      CUSTOMER         DIETITIAN          OPS
        APP             DASHBOARD       DASHBOARD
          │                │                │
          └────────────────┼────────────────┘
                           │
                       COURIER
                       INTERFACE
```

## 1. Customer Application — Core Product

The customer application is **P0 and mandatory** in Phase 1. It is not a generic grocery-shopping interface.

Its purpose is to become the customer's digital home for the new lifestyle they are building with their dietitian/fitness professional.

### P0

| Feature | Purpose |
|---|---|
| Registration/login | Low-friction onboarding from a dietitian or gym invite |
| Profile | Identity, address/map pin, allergies/intolerances, dislikes, household size, delivery preferences |
| Dietitian connection | Make the professional relationship visible and persistent |
| Nutrition plan | Show the current plan in a simple, readable format |
| Weekly basket | Show exactly what Nuvia will source, quantities and itemised price |
| Basket approval | Customer approves or skips; alternatives only from dietitian-approved options |
| Delivery window | Clear expected delivery day/window |
| Order tracking | Preparing → out for delivery → delivered |
| Payment state | Clearly show **“Payment due at delivery”** before the courier arrives |
| Delivery-day payment | Show exact amount due and payment confirmation after courier SoftPOS transaction |
| Subscription controls | Pause, skip, resume, cancel |
| Receipts/history | Past orders and payment references |
| Support | Direct route to Nuvia operations |

### P1

- Progress tracking visible to the dietitian.
- Adherence streak / consecutive weeks.
- Simple weekly adherence summary.

### Product principle

The customer should **not** have to behave like a shopper.

```text
Traditional grocery app:
Customer decides → searches → compares → builds cart → pays

Nuvia:
Professional plans → Nuvia builds basket → customer reviews →
customer approves → Nuvia delivers → customer pays at the door
```

The reduction in decision load is part of the product value.

---

## 2. Dietitian Dashboard — Free Professional Product

The dietitian dashboard is also **P0**.

In Phase 1, it is offered as a free professional tool to make Nuvia useful before the logistics revenue is large enough to matter.

### P0

| Feature | Purpose |
|---|---|
| Client management | Add/invite clients and see active/paused/churned state |
| Nutrition plan creation | Create weekly plans and reusable templates |
| Plan versioning | Know which plan produced each basket |
| Basket review | Review/confirm the products and quantities generated from a plan |
| Retention view | See consecutive weeks, skips, approvals and last delivery |
| Action list | Identify clients who have not approved or are falling inactive |
| Order history | See client orders and delivery status |
| Commission ledger | Completed-order earnings, payout history and status |

### P1

- Bulk order generation.
- More detailed adherence analytics.
- Practice-level retention reporting.

### Strategic purpose

Nuvia should be presented to dietitians primarily as:

> **A free tool that helps you manage clients, turn plans into actionable weekly baskets, and keep clients engaged.**

The ~5% completed-order commission is a secondary incentive, not the primary pitch.

The goal is to create a flywheel:

```text
Dietitian joins for free software
        ↓
Adds clients
        ↓
Creates plans in Nuvia
        ↓
Clients use Nuvia customer app
        ↓
Weekly baskets are generated
        ↓
Customers reorder
        ↓
Dietitian sees better continuity + earns commission
        ↓
Dietitian keeps Nuvia in their workflow
```

Nuvia does not make clinical/nutritional decisions on behalf of the dietitian. The professional owns the plan; Nuvia executes the supply and logistics layer.

---

## 3. Operations Dashboard

The internal control plane.

### P0

- Weekly order board.
- Supplier pick-list aggregation.
- Supplier acceptance/readiness status.
- Courier assignment.
- Route assembly and time windows.
- Customer support context.
- Payment/settlement reconciliation.
- Complaint and exception handling.
- Pilot metrics.

### P1

- Supplier/courier performance history.
- More automated route assistance.

---

## 4. Courier Interface

Mobile web/PWA is sufficient in Phase 1.

### P0

- Today's route.
- Stops in order.
- Known addresses/map pins.
- Delivery windows.
- Supplier pickup checklist.
- Expected route pay.
- Customer delivery notes.
- SoftPOS payment flow/reference.
- Delivery confirmation.
- Failure/refusal reporting.

### Core courier value proposition

The courier knows the route before starting work:

```text
Known stops
Known addresses
Known time windows
Known route
Known expected pay
```

Nuvia is not competing with instant-delivery platforms on speed. It is selling **predictability and route density**.

---

# Phase 1 Payment Model

Customer payment is **not prepaid** in the standard flow.

```text
Customer approves basket
        ↓
Supplier prepares
        ↓
Courier collects goods
        ↓
Courier delivers
        ↓
Customer sees package
        ↓
Customer pays via courier SoftPOS
        ↓
Payment confirmed
        ↓
Settlement begins
```

The target is for the supplier's payable and other eligible shares to be settled automatically and quickly after successful payment. **~30 minutes is the operational target to negotiate/validate, not a guaranteed banking SLA.**

The supplier must explicitly agree to release goods before customer payment under an agreed exposure/settlement policy.

Detailed payment decisions belong in [`PAYMENT_AND_SETTLEMENT.md`](./PAYMENT_AND_SETTLEMENT.md).

---

# Phase 2: Micro Fulfilment Centre

Move from multi-supplier pickup to a central facility.

```text
Phase 1:
Supplier A ─┐
Supplier B ─┼─> Courier ─> Customer
Supplier C ─┘

Phase 2:
Wholesale suppliers → Micro fulfilment centre → Courier → Customer
```

Goals:

- Wholesale purchasing.
- Lower food cost.
- Centralised portioning/packing.
- Quality control.
- Cold-chain control.
- Single-origin courier routes.
- Inventory and waste management.

Phase 2 is where Nuvia begins to exploit the demand forecast created by Phase 1.

## Exit Criteria

- COGS reduction ≥15% versus Phase 1 baseline.
- Quality complaint rate <2%.
- Facility capable of 500+ weekly packages.
- Positive steady-state contribution margin.
- Route cost per delivery reduced ≥20% through single-origin dispatch.

---

# Phase 3: Nutrition Production Company

Move from raw ingredient supply to prepared personalised meals.

The information advantage already exists:

```text
Known customer
+ known dietitian
+ known plan
+ known weekly demand
= predictable meal production demand
```

Product lines can include weight-management, muscle/performance and hybrid prepared + raw plans, subject to qualified professional oversight and applicable food regulations.

The positioning remains:

> **Personalised nutrition infrastructure, not generic catering.**

## Exit Criteria

- Prepared-meal gross margin >35%.
- Prepared-meal line ≥40% of revenue.
- Multi-district operation stable in Samsun.
- Repeatable city-launch playbook.
- Clean food-safety record.

---

# Phase 4: Network Expansion

Replicate the playbook into additional Samsun districts, then comparable cities.

What transfers:

- Software.
- Brand.
- Dietitian acquisition playbook.
- Operating procedures.
- Product specifications.
- Courier model.

What must be rebuilt locally:

- Suppliers.
- Couriers.
- Dietitian relationships.
- Fulfilment capacity.

Local density and trust remain core to the model.
