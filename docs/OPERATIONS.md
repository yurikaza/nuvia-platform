# Operations — Phase 1

> Phase 1 operations are deliberately **semi-manual**. A human operations coordinator sits in the middle of every loop. This is correct: manual operations reveal what actually needs automating, and automating too early hard-codes the wrong process.

---

## 1. Core Workflow

```
                          CUSTOMER
                              │
                              ▼
              ┌──────────────────────────────┐
              │  DIETITIAN CREATES PLAN      │
              │  weekly meal structure,      │
              │  foods, quantities           │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  SYSTEM GENERATES            │
              │  WEEKLY ORDER                │
              │  plan → basket, priced       │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  CUSTOMER APPROVES PACKAGE   │
              │  review, swap, skip, confirm │
              │  ── HARD CUTOFF ──           │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  SUPPLIER PREPARES PRODUCTS  │
              │  consolidated pick list,     │
              │  portioned to spec           │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  COURIER RECEIVES ROUTE      │
              │  stops, sequence, windows,   │
              │  expected pay                │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  DELIVERY COMPLETED          │
              │  confirmed, photo optional   │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  PAYMENT CONFIRMED           │
              │  charge settled;             │
              │  commission accrued          │
              └───────────────┬──────────────┘
                              ▼
              ┌──────────────────────────────┐
              │  CUSTOMER CONTINUES          │
              │  SUBSCRIPTION                │
              │  next week's basket generated│
              └───────────────┬──────────────┘
                              │
                              └──────► loops back to weekly order
```

---

## 2. Weekly Operating Calendar

Fixed cadence. Everyone — customers, dietitians, suppliers, couriers — knows the rhythm. Predictability is the product.

| Day | Time | Who | Action |
|---|---|---|---|
| **Thursday** | 09:00 | System | Generate next week's baskets from active plans |
| **Thursday** | 10:00 | Dietitians | Review and confirm baskets for their clients |
| **Thursday** | 12:00 | System | Send baskets to customers; approval window opens |
| **Thu–Fri** | — | Customers | Review, swap, approve or skip |
| **Friday** | **18:00** | — | **APPROVAL CUTOFF.** No changes after this point. |
| **Friday** | 19:00 | System | Aggregate approved baskets into per-supplier pick lists |
| **Friday** | 20:00 | Ops | Send pick lists to suppliers; confirm acceptance |
| **Saturday** | 09:00 | Ops | Build routes, assign couriers, publish routes |
| **Saturday** | 10:00 | Couriers | Routes visible; confirm shift |
| **Sunday** | 08:00 | Suppliers | Orders prepared and ready for pickup |
| **Sunday** | 09:00 | Couriers | Collect from suppliers, verify against manifest |
| **Sunday** | 10:00–16:00 | Couriers | **Delivery window** |
| **Sunday** | 17:00 | Ops | Reconcile: deliveries, failures, cash collected |
| **Monday** | 10:00 | Ops | Handle complaints, issue refunds, follow up failures |
| **Monday** | 14:00 | Ops | Pay couriers; reconcile supplier invoices |
| **Tuesday** | 10:00 | Ops | Weekly metrics review; partner check-ins |
| **Wednesday** | — | Ops | Partner visits, new-customer onboarding, supplier meetings |

**Delivery days:** Phase 1 runs a single Sunday delivery day. Add a second day (Wednesday) only when routes exceed ~20 stops. Consolidating days maximises route density, which is the primary margin lever ([`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) §4).

**The cutoff is sacred.** Every exception granted after 18:00 Friday cascades into supplier confusion, route rework, and a late delivery. Say no. Offer next week instead.

---

## 3. Stage Detail

### 3.1 Plan Creation (Dietitian)

The dietitian builds a weekly plan: meals per day, foods and quantities per meal, accounting for the client's allergies, dislikes, household size and budget band.

**Plan → basket conversion.** The system maps plan items to purchasable supplier products and rounds to realistic purchase units (500g packs, dozen eggs, 1kg bags). Two rules govern this:
- Never round down below the plan requirement
- Flag any item with no supplier product match for manual resolution

Plans are reusable templates cloned per client. Without templates the dietitian workflow is too slow to survive contact with a real practice.

### 3.2 Order Generation (System)

Thursday 09:00, for every active, unpaused subscription:
1. Load the current plan
2. Expand to a 7-day ingredient requirement
3. Map to supplier products, apply purchase-unit rounding
4. Subtract pantry staples the customer has flagged as already stocked
5. Price the basket
6. Flag unavailable or out-of-season items with allowed alternatives
7. Route to the dietitian for confirmation

**Ops watches for:** baskets outside the 1,200–2,400 TL band (likely a plan error), unmatched items, and any customer whose basket changed >25% week over week.

### 3.3 Customer Approval

The customer sees the item list with quantities and prices, the total, and their delivery window. They can swap flagged items within dietitian-allowed alternatives, skip the week, or approve.

- **Reminder at Friday 12:00** to anyone who has not acted
- **No response by cutoff:** the week is skipped, not auto-charged. Auto-charging without approval destroys trust and is not worth the incremental order.
- Ops calls anyone who has skipped two consecutive weeks — that is the churn signal, and it is recoverable if caught in the same week.

### 3.4 Supplier Preparation

Friday 19:00, approved baskets aggregate into one pick list per supplier:

```
BUTCHER — Sunday 08:00 pickup
  Chicken breast, 180g portions ......... 156 portions (28.1 kg)
  Beef mince, 5% fat, 250g .............. 42 packs (10.5 kg)
  Turkey breast, 150g portions .......... 28 portions (4.2 kg)
```

Ops sends the list (WhatsApp is acceptable in Phase 1) and requires explicit acceptance. Any shortfall must be reported by Saturday 12:00 so substitutions can be arranged and affected customers notified before delivery day — never on delivery day.

**Portioning is the point.** Portioned products are the core of the value proposition; unportioned bulk is just groceries. Portion tolerance and labelling are contractual, not requests.

### 3.5 Route Planning

Saturday 09:00. Ops clusters approved deliveries geographically, sequences stops, and assigns to couriers.

Constraints: 10–20 stops per route, cold-chain time limits (chilled goods should reach the last customer within ~4 hours of pickup), customer time-window preferences, and courier availability.

Phase 1 implementation: map view with manual clustering plus a nearest-neighbour ordering heuristic. Good enough at this volume; full optimisation is a Phase 2 problem.

Routes publish to couriers Saturday 10:00 — **before** the shift, always. That advance visibility is the entire courier value proposition.

### 3.6 Delivery

Courier collects from suppliers, verifying each item against the manifest before leaving. A discrepancy caught at pickup is a solved problem; the same discrepancy caught at a customer's door is a complaint.

At each stop: deliver, confirm in the app, take a photo if the customer is absent and has authorised drop-off, collect cash if applicable.

**Failed delivery:** the courier records a reason code and moves on — never wait more than 5 minutes. Ops contacts the customer immediately and arranges same-day retry if the route allows, otherwise a refund or credit.

### 3.7 Payment

Default is **card, charged on approval** (Friday). This eliminates delivery-day payment friction and surfaces payment failures two days before the food is bought.

Cash on delivery is available on request in Phase 1 — trust is not yet established and refusing cash costs real customers in this market. Couriers reconcile cash Sunday evening.

On a failed card charge: retry once, notify the customer, and if unresolved by Saturday 09:00, remove the order from the routes. Never deliver an unpaid order in Phase 1.

Dietitian commission accrues on delivery confirmation and pays monthly.

### 3.8 Subscription Continuity

The subscription is the default state — the next basket generates automatically. The customer never re-decides to be a customer; they only decide to stop.

**Churn signals ops must act on within the same week:**

| Signal | Action |
|---|---|
| Skipped 2 consecutive weeks | Phone call from ops |
| No approval before cutoff, twice | Phone call |
| Quality complaint | Same-day resolution + follow-up next week |
| Failed delivery | Immediate contact + goodwill credit |
| Progress tracking stopped | Flag to the dietitian |
| Basket value dropping steadily | Flag to the dietitian — the plan may not fit |

---

## 4. Supplier Management

### Selection

| Criterion | Requirement |
|---|---|
| Consistency | Reliability beats price. A cheap supplier who fails once has cost more than the discount. |
| Portioning | Willing and able to portion to our spec, labelled |
| Hygiene | Visibly clean, cold chain maintained, proper storage |
| Capacity | Headroom for 3–5× current volume |
| Communication | One named contact, reachable, responsive on WhatsApp |
| Proximity | Inside or adjacent to Atakum, to keep pickup routes short |

**Deliberately few suppliers.** 2–4 total in Phase 1. Every additional supplier is another pickup stop, another quality variable, and another relationship to maintain.

### Agreement Terms

Pricing for a fixed term (3 months) with a review clause; portion specs and tolerances; a written quality spec per product; pickup-ready times; a shortfall protocol; and payment terms (weekly, on invoice, paid on time — this is how we stay the customer they prioritise).

### Ongoing

- Weekly: send the pick list, confirm acceptance, log any shortfall
- Weekly: log any quality complaint against the responsible supplier
- Monthly: visit in person, review complaint rate, discuss upcoming volume
- Quarterly: pricing review, spec review

**Never single-source a critical category.** Have a named backup for chicken and red meat even if it is never used.

---

## 5. Quality Control

Quality inconsistency is the highest-severity operational risk in Phase 1 ([`RISKS_AND_MITIGATION.md`](./RISKS_AND_MITIGATION.md), Risk 3). Every stage has a check.

| Checkpoint | Who | What |
|---|---|---|
| **Supplier selection** | Ops | Site visit, hygiene inspection, sample order before signing |
| **Spec definition** | Ops | Written spec per product: cut, fat ratio, portion weight and tolerance, freshness, packaging, labelling |
| **Pickup verification** | Courier | Item count, visible condition, temperature, correct labelling — before leaving the supplier |
| **Spot audit** | Ops | Physically inspect 2–3 random baskets per delivery day |
| **Delivery confirmation** | Courier | Condition on handover; photo on drop-off |
| **Customer feedback** | Customer | One-tap rating post-delivery; complaint flow in app |
| **Weekly review** | Ops | Complaints by supplier and by product; act on any pattern |

**Complaint handling — resolve, then diagnose:**
1. Acknowledge within 2 hours
2. Refund or replace the item, no argument, on the first complaint
3. Log against the supplier and product
4. Follow up the next week to confirm it did not recur
5. Two complaints on the same product from the same supplier in a month → formal conversation. Persisting → replace the supplier.

**Cold chain:** insulated bags with ice packs; chilled goods delivered within ~4 hours of pickup; sequence chilled-heavy stops earliest in the route; couriers trained never to leave bags in direct sun.

**Standard:** a customer should never have to decide whether an item is acceptable. If they are inspecting, we have already failed.

---

## 6. Delivery Scheduling

**Fixed weekly delivery day** (Sunday, 10:00–16:00) in Phase 1. Customers choose a preferred 2-hour window inside it; windows are honoured where routing allows, and the customer is told the actual window Saturday evening.

**Rules:**
- Density beats convenience. Offering seven delivery days would halve route density and double cost per drop.
- Notify actual windows the evening before, and again when the courier is en route.
- Absent-customer policy: authorised drop-off (neighbour, doorman, door) is recorded at signup; without authorisation, a 5-minute wait then a failed-delivery record.
- Address quality matters — Atakum addressing is inconsistent, so a map pin is mandatory at signup and delivery notes are captured on the first successful delivery.

**Scaling:** at ~20 stops per route, add a second courier before adding a second day. At two couriers per day saturated, add a Wednesday delivery. Splitting into more days too early is the most common way to destroy delivery economics.

---

## 7. Customer Support

**Channels:** in-app support button (WhatsApp deeplink is acceptable in Phase 1), a WhatsApp business line, and phone for urgent delivery-day issues. Response targets: delivery-day issues within 30 minutes; everything else within 4 hours during business hours.

**Common cases and the standing resolution:**

| Case | Resolution |
|---|---|
| Missing item | Refund the item immediately; replace next delivery |
| Quality problem | Refund or replace, no argument, first time |
| Wrong quantity | Refund the difference; log against supplier |
| Late delivery | Proactive notification before the customer asks; credit if severe |
| Failed delivery | Same-day retry if possible, otherwise full refund |
| Want to change plan | Route to their dietitian — never change plan content ourselves |
| Want to pause | Self-service in the app; ops asks why only if it becomes two weeks |
| Want to cancel | Do not fight it. Ask one question: *why?* That answer is the most valuable data the pilot produces. |

**Escalation:** anything involving illness or food safety goes to a founder immediately, with the batch and supplier identified the same day.

**Proactive support is cheaper than reactive.** Notifying a customer about a delay before they notice converts a complaint into a trust event.

---

## 8. Roles

| Role | Who (Phase 1) | Responsibility |
|---|---|---|
| Operations coordinator | 1 part-time hire | The weekly calendar end to end: pick lists, routes, complaints, reconciliation |
| Partner manager | Founder | Dietitian, gym, and supplier relationships |
| Product / engineering | Founder | The four software surfaces |
| Couriers | 3 contractors | Delivery |
| Suppliers | 2–4 partners | Preparation and portioning |

Founders should personally run a delivery route and handle support at least once per month during the pilot. Every serious operational insight in Phase 1 will come from the road, not the dashboard.

---

## 9. Escalation Thresholds

| Situation | Action |
|---|---|
| Supplier cannot fulfil | Substitute from backup; notify affected customers **before** delivery day; never surprise them at the door |
| Courier does not show | Ops runs the route personally. The route always runs. |
| Payment system down | Deliver anyway; collect after. Do not break the week. |
| Quality incident (illness) | Halt that product line immediately; contact every customer who received the batch; founder-led |
| Route cannot complete | Prioritise chilled goods; reschedule the rest same day; refund and apologise proactively |
| >5 complaints in one delivery day | Full post-mortem before the next cycle; do not run another week on the same process |
