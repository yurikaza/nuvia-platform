# Product Roadmap

Three phases, each with one question to answer. A phase does not start until the previous phase's question is answered with evidence.

| Phase | Horizon | Question being answered | Model |
|---|---|---|---|
| **1 — Atakum Pilot** | Months 0–6 | Will customers reorder a plan-linked package? | Supplier + courier network |
| **2 — Micro Fulfilment** | Months 6–18 | Can we control cost and quality at volume? | Centralised inventory |
| **3 — Nutrition Production** | Months 18–36 | Will customers buy prepared personalised meals? | Production company |

---

# Phase 1: Atakum Pilot

## Goal

Validate the business model with a small, controlled operation. **This phase is not about growth or profit.** It is about producing evidence that the loop closes: plan → order → delivery → payment → reorder.

Anything that does not produce that evidence is out of scope.

## Targets

| Target | Number | Rationale |
|---|---|---|
| Dietitian partners | 10 signed, 5+ actively generating orders | 10 signed is realistic for Atakum; the meaningful number is how many actually use it |
| Fitness centre partners | 2–3 | Enough to test the channel without diluting focus |
| Active customers | 50–100 | Below 50 route density is untestable; above 100 manual operations break |
| Delivery partners (couriers) | 2–3 | 2 covers the routes, the 3rd is redundancy |
| Suppliers | 2–4 | Deliberately few — quality control over catalogue breadth |
| Districts | 1 (Atakum only) | Density is the entire delivery economics argument |

## Success Criteria (gate to Phase 2)

- ≥40% of customers who complete week 1 also complete week 4
- ≥5 dietitians generating orders in the final month without prompting
- Contribution margin per delivery ≥ 0 at ≥60 active customers
- Quality complaint rate <5% of deliveries
- Net customer sentiment positive in structured week-8 interviews

Full measurement plan: [`VALIDATION_PLAN.md`](./VALIDATION_PLAN.md).

---

## Phase 1 Features

Four surfaces. Everything below is scoped to the minimum that makes the loop work. Technical detail: [`MVP_TECHNICAL_REQUIREMENTS.md`](./MVP_TECHNICAL_REQUIREMENTS.md).

### 1. Customer Application

| Feature | Description | Priority |
|---|---|---|
| **Registration** | Phone/SMS or email signup. Invite code from a dietitian or gym is the primary entry path. | P0 |
| **Profile** | Name, delivery address (with map pin — Atakum addressing is inconsistent), phone, allergies/intolerances, dislikes, household size, preferred delivery window. | P0 |
| **Dietitian connection** | Link to the dietitian who invited them; see who their professional is. One dietitian per customer in Phase 1. | P0 |
| **Nutrition plan viewing** | Read-only view of the current plan: weekly meal structure, what to eat when. Not a plan editor. | P0 |
| **Weekly package approval** | The core interaction. See the generated basket (items, quantities, price), swap flagged items within allowed alternatives, approve or skip the week. Hard cutoff time. | P0 |
| **Payment** | Card payment per weekly package via a Turkish PSP. Saved card for recurring weeks. Clear itemised price. | P0 |
| **Order tracking** | Status: approved → preparing → out for delivery → delivered. Delivery window, courier contact on delivery day. | P0 |
| **Subscription management** | Pause a week, skip a week, change delivery window, change address, cancel. Self-service — never a phone call. | P0 |
| **Progress tracking** | Weight and optional body measurements, simple chart, visible to their dietitian. Adherence streak (consecutive weeks). | P1 |
| Notifications | SMS/push: basket ready for approval, approval cutoff reminder, out for delivery, delivered. | P0 |
| In-app support | One button to reach operations (WhatsApp deeplink is acceptable in Phase 1). | P1 |

**Explicitly out of scope in Phase 1:** recipes, calorie/macro logging, photo food diaries, social features, gamification, chat with dietitian (they already have WhatsApp), multi-address, gifting, referral programs.

### 2. Dietitian Dashboard

| Feature | Description | Priority |
|---|---|---|
| **Customer management** | Add a client (generates an invite), see all clients, status per client (active / pending / paused / churned), client detail view. | P0 |
| **Nutrition plan creation** | Build a weekly plan: meals per day, foods and quantities per meal. Save as a reusable template; clone and adjust per client. Template library is what makes this fast enough to actually be used. | P0 |
| **Order generation** | Convert a plan into a weekly basket: system proposes the item list and quantities from the plan, dietitian reviews and confirms, order is sent to the customer for approval. | P0 |
| **Customer retention analytics** | Per client: consecutive weeks, approval rate, skipped weeks, last delivery, progress trend. Practice-level: active clients, average client lifespan, churn list. This is the screen that proves our value proposition to them. | P0 |
| **Commission tracking** | Earned per completed order, monthly total, payout status and history. | P0 |
| Adherence signals | Which clients skipped this week, which have not approved before cutoff. A short daily action list. | P1 |
| Bulk actions | Generate orders for all clients at once. Essential once a dietitian passes ~15 clients. | P1 |

### 3. Operations Dashboard

Internal. The most important surface in Phase 1 — it is where the business is actually run.

| Feature | Description | Priority |
|---|---|---|
| **Order management** | All orders for the week by state. Manual intervention on any order. Flag problems. | P0 |
| **Supplier coordination** | Aggregate all approved baskets into a per-supplier pick list (e.g. "Butcher: 42kg chicken breast in 180g portions"). Export/print/WhatsApp-able. Confirm supplier acceptance and readiness. | P0 |
| **Delivery assignment** | Assign orders to couriers and delivery days. See load per courier. | P0 |
| **Route planning** | Cluster deliveries geographically, order the stops, produce a route with addresses and time windows. Phase 1 acceptable implementation: map view + manual sequencing with a distance heuristic. Full optimisation is Phase 2. | P0 |
| Customer support view | Full context for one customer: orders, payments, deliveries, complaints. | P0 |
| Payment reconciliation | Which orders are paid, failed, refunded. Supplier invoices, courier payouts, dietitian commissions. | P0 |
| Basic metrics | Active customers, weekly orders, reorder rate, cost per delivery, complaint rate. The pilot scoreboard. | P0 |
| Supplier & courier records | Contacts, terms, pricing, performance notes. A spreadsheet is acceptable at ≤4 suppliers. | P1 |

### 4. Courier Interface

Mobile web is sufficient. Do not build native apps in Phase 1.

| Feature | Description | Priority |
|---|---|---|
| **Delivery list** | Today's assigned deliveries, in route order, with total count and expected pay. Visible before the shift starts — this is the core of the courier value proposition. | P0 |
| **Route information** | Ordered stop list, map link per stop, estimated duration. | P0 |
| **Customer address** | Address, map pin, delivery notes (floor, buzzer, "call on arrival"), masked phone number. | P0 |
| **Delivery confirmation** | Mark delivered; optional photo; failed-delivery reason codes. | P0 |
| **Payment confirmation** | For cash-on-delivery orders: record amount collected. Prepaid orders show as already paid. | P0 |
| Pickup checklist | Confirm collection from each supplier before starting the route. | P1 |

---

# Phase 2: Micro Fulfilment Centre

## The Shift

**From:** orders routed to multiple suppliers, each preparing per-order, courier collecting from several points.

**To:** a single small facility that holds inventory, receives wholesale deliveries, portions and packs centrally, and dispatches from one point.

```
PHASE 1                              PHASE 2
                                     
Order ──┬─> Butcher ──┐              Wholesale ──> ┌─────────────┐
        ├─> Chicken ──┼─> Courier    suppliers     │   MICRO     │
        ├─> Market  ──┤   (multi-                  │ FULFILMENT  │──> Courier
        └─> Grocer  ──┘    pickup)   Order ───────>│   CENTRE    │    (single
                                                   │ stock•pack  │     pickup)
Variable quality per supplier                      └─────────────┘
Retail-ish pricing                                 Controlled quality
Multi-stop pickup overhead                         Bulk pricing
```

## Why

**Bulk purchasing.** Buying weekly aggregate volume wholesale instead of order-by-order at supplier prices. This is the single largest margin lever available — a 15–25% COGS reduction is realistic and turns a thin Phase 1 contribution into a real one.

**Better margins.** Beyond purchase price: less waste through pooled inventory, no per-order supplier handling premium, and a courier route that starts at one location instead of four.

**Quality control.** We own portioning, packing, cold chain, and inspection. In Phase 1 quality is a supplier promise; in Phase 2 it is a process we run. This directly addresses the highest-severity Phase 1 risk.

**Faster preparation.** Batch processing on our own schedule, decoupled from supplier opening hours. Same-day order changes become possible, and delivery windows tighten.

## Requirements

- Facility: small commercial unit in or near Atakum, ~80–150 m², with refrigeration and freezer capacity, hygiene-compliant, licensed for food handling
- Staff: 2–4 fulfilment operators plus a supervisor
- Systems: inventory management, stock levels and reorder points, wastage tracking, batch/lot traceability, goods-in inspection
- Compliance: food business registration, hygiene certification, cold-chain records, staff health certificates
- Capital: fit-out, refrigeration, packing equipment, initial working capital for inventory

## New / Changed Software

| Area | Change |
|---|---|
| Inventory | Stock levels, reorder points, expiry and batch tracking, wastage |
| Purchasing | Demand forecast from approved baskets → purchase orders to wholesale suppliers |
| Fulfilment | Pick-and-pack workflow, per-order packing checklist, barcode or label scanning |
| Route planning | Real optimisation from one origin; time-window constraints |
| Quality | Goods-in inspection records, complaint linkage back to batch |

## Exit Criteria (gate to Phase 3)

- COGS reduction ≥15% versus Phase 1 baseline
- Quality complaint rate <2% of deliveries
- Facility capable of 500+ weekly packages
- Positive contribution margin at steady state
- Route cost per delivery reduced ≥20% via single-origin dispatch

---

# Phase 3: Nutrition Production Company

## The Shift

**From:** delivering raw ingredients that the customer cooks.

**To:** delivering prepared, personalised meals — while keeping raw supply available for customers who want to cook.

This is not a pivot away from the model; it is the model's natural end state. We already know, a week in advance, exactly what each customer is supposed to eat. Producing it is the highest-value thing we can do with that information.

## Product Lines

**Weight-loss meal plans.** Calorie- and portion-controlled full-day or partial-day meal sets, built from the customer's dietitian plan. High volume, high adherence sensitivity.

**Muscle-gain plans.** Protein-forward, higher-calorie meal sets with defined macro targets, structured around training days.

**Performance nutrition packages.** Athlete and serious-trainee packages: pre/post-training nutrition, timing-specific meals, competition-period plans. Highest price point, strongest word-of-mouth in the fitness-centre channel.

**Hybrid (expected to dominate).** Prepared lunches and dinners plus raw ingredients for breakfasts and snacks. Most customers do not want every meal handed to them — habit formation requires that they still cook some of the time.

## Positioning

**We are a personalised nutrition company, not a catering company.** The distinction is commercial, not cosmetic:

| | Diet catering | Nutrition Lifestyle Network |
|---|---|---|
| Menu | Fixed weekly menu for everyone | Derived from the individual's plan |
| Professional | None, or an in-house nutritionist | The customer's own dietitian |
| Goal | Serve meals | Sustain a habit and produce a measurable outcome |
| Data | None | Adherence and progress, fed back to the professional |
| Relationship | Vendor | Part of the customer's health team |
| Ends when | The customer gets bored | The customer reaches their goal — and often continues at maintenance |

Catering is a commodity that competes on price and menu variety. We compete on personalisation and outcome, which is defensible and higher margin.

## Requirements

- Licensed production kitchen (upgrade or replacement of the Phase 2 facility)
- Chefs, food production staff, a food safety officer
- Menu R&D: a library of meals mapped to macro and calorie targets, and to plan constraints
- Cold-chain distribution capable of prepared-meal safety standards
- Full food-safety compliance and HACCP-equivalent process

## New / Changed Software

| Area | Change |
|---|---|
| Meal engine | Map a nutrition plan to producible meals meeting its macro/calorie constraints |
| Production planning | Aggregate meal demand → production schedule, prep sheets, yield planning |
| Recipe & BOM | Recipes, ingredient bills of materials, cost per meal, allergen matrix |
| Traceability | Batch → meal → customer, for recall and complaint handling |
| Dietitian tooling | Approve or adjust the meal mapping for their client; substitution rules |

## Exit Criteria (gate to Phase 4 expansion)

- Prepared-meal gross margin >35%
- Prepared-meal line ≥40% of revenue
- Multi-district operation stable in Samsun
- A documented, repeatable city-launch playbook
- Food safety record clean

---

# Phase 4: Network Expansion (Outline)

Replicate into Samsun districts (İlkadım, Canik, Tekkeköy), then comparable Anatolian cities of 300k–1M population with a compact residential core, a university, and an active fitness culture.

**What transfers:** software, the dietitian-partnership playbook, the route model, supplier standards and specs, the brand.

**What is rebuilt locally:** suppliers, couriers, dietitian relationships, the fulfilment facility. This is intentional — local trust is the moat, and it cannot be shipped from another city.

**Launch sequence per city:** dietitian recruitment first, then suppliers, then couriers, then customers. Never launch a city before 5 active dietitians exist in it.
