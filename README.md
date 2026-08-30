# Nuvia Platform

> **Working title.** A localized nutrition logistics platform connecting dietitians, fitness centres, customers, local suppliers, and planned delivery partners.
>
> **Pilot location:** Atakum, Samsun, Turkey.

---

## Positioning

> ### We are not a fast delivery company. We are a planned nutrition logistics network.

Speed is not the product. **Consistency is.** Nuvia closes the gap between a professional nutrition plan and actually having the required food at home.

## What This Is

People often do not need another nutrition plan. The difficult part is executing the plan repeatedly: shopping, sourcing, portioning, remembering what to buy, and keeping the routine alive.

Nuvia connects the professional plan to the physical supply chain:

```text
Dietitian / fitness professional
            ↓
     Personalized plan
            ↓
      Nuvia basket
            ↓
 Local suppliers prepare
            ↓
 Planned courier route
            ↓
 Customer receives package
            ↓
 Customer pays via SoftPOS
            ↓
 Settlement + next week's plan
```

The customer is not expected to behave like a grocery shopper. The professional defines the plan; Nuvia handles the execution layer.

---

## The Product Is Two-Sided

### Customer application

The customer app is a **core Phase 1 product**, not a later convenience feature. It is the customer's digital home for the lifestyle program:

- dietitian relationship;
- nutrition plan;
- weekly basket;
- approval/skip;
- delivery status;
- payment-at-delivery status;
- SoftPOS receipt/history;
- subscription controls;
- later, progress/adherence.

The customer approves the basket before preparation but **pays when the package reaches them**, using the courier's SoftPOS device. This is designed to reduce the uncertainty of paying before seeing the physical package.

### Dietitian professional tool

The dietitian dashboard is also a **core Phase 1 product and free for pilot partners**.

It lets professionals:

- manage clients;
- create reusable nutrition plans;
- review generated baskets;
- see adherence/retention signals;
- follow client order history;
- earn approximately 5% on completed eligible orders.

The primary pitch is **not commission**. It is:

> **A free tool that helps you manage clients, turn plans into actionable weekly baskets, and keep clients engaged.**

This creates the core acquisition flywheel:

```text
Dietitian joins for free tooling
        ↓
Adds clients
        ↓
Creates plans
        ↓
Clients enter Nuvia app
        ↓
Weekly baskets are executed
        ↓
Customers reorder
        ↓
Dietitian gets retention + adherence visibility + commission
        ↓
Dietitian keeps using Nuvia
```

Nuvia does not make clinical/nutritional decisions. The dietitian owns the professional plan; Nuvia owns execution and logistics.

---

## Why Atakum

Atakum is the initial **working hypothesis for the best pilot density**, based on its residential, university and fitness characteristics. Income distribution and willingness to pay must be validated rather than treated as proven facts.

The pilot deliberately remains inside one district because route density is central to the economics.

---

## Participants

| Participant | Gives | Gets |
|---|---|---|
| **Customer** | Weekly commitment + delivery-time payment | Plan-linked supply, low decision load, predictable delivery |
| **Dietitian** | Professional plan + clients | Free software, retention/adherence visibility, ~5% completed-order commission |
| **Fitness centre** | Member referrals | A complete transformation support layer |
| **Local supplier** | Prepared/portioned goods | Predictable weekly volume and short, agreed settlement cycle |
| **Courier** | Planned route delivery + SoftPOS acceptance | Known route, stops, time windows and expected pay |
| **Nuvia** | Coordination + customer relationship | Platform margin and recurring demand |

The model works when every participant has a reason to support **customer continuity**.

---

## Roadmap

| Phase | Horizon | Question | Model |
|---|---|---|---|
| **1 — Atakum Pilot** | Months 0–6 | Will customers reorder plan-linked baskets and will partners keep using Nuvia? | Local suppliers + planned couriers |
| **2 — Micro Fulfilment** | Months 6–18 | Can we control cost and quality at volume? | Wholesale + central fulfilment |
| **3 — Nutrition Production** | Months 18–36 | Will customers buy prepared personalised meals? | Nutrition production company |
| **4 — Network Expansion** | Months 36+ | Can the playbook transfer? | Local network replication |

**Phase 1 target:** 10 dietitian partners · 2–3 fitness centres · 50–100 active customers · 2–3 couriers · 2–4 suppliers · Atakum only.

Phase 1 is intentionally a validation phase, not a maximum-profit phase.

---

## Documentation

The `/docs` directory is the source of truth.

| # | Document | Purpose |
|---|---|---|
| 1 | **[PROJECT_OVERVIEW.md](./docs/PROJECT_OVERVIEW.md)** | Problem, opportunity, vision and positioning |
| 2 | **[BUSINESS_MODEL.md](./docs/BUSINESS_MODEL.md)** | Participants, incentives, revenue model and assumptions |
| 3 | **[PRODUCT_ROADMAP.md](./docs/PRODUCT_ROADMAP.md)** | Product surfaces and Phase 1–4 evolution |
| 4 | **[UNIT_ECONOMICS.md](./docs/UNIT_ECONOMICS.md)** | Package economics, delivery economics and assumptions |
| 5 | **[PARTNER_ACQUISITION.md](./docs/PARTNER_ACQUISITION.md)** | Dietitian, gym, supplier and courier acquisition |
| 6 | **[OPERATIONS.md](./docs/OPERATIONS.md)** | Weekly operating workflow |
| 7 | **[PAYMENT_AND_SETTLEMENT.md](./docs/PAYMENT_AND_SETTLEMENT.md)** | SoftPOS delivery payment and settlement model |
| 8 | **[RISKS_AND_MITIGATION.md](./docs/RISKS_AND_MITIGATION.md)** | Risks, mitigations and kill signals |
| 9 | **[MVP_TECHNICAL_REQUIREMENTS.md](./docs/MVP_TECHNICAL_REQUIREMENTS.md)** | Architecture and MVP build scope |
| 10 | **[VALIDATION_PLAN.md](./docs/VALIDATION_PLAN.md)** | Discovery, pilot and go/no-go criteria |

---

## Phase 1 Payment Model

```text
Customer approves basket
        ↓
Supplier prepares
        ↓
Courier collects from supplier(s)
        ↓
Courier delivers
        ↓
Customer sees package
        ↓
Customer pays via courier SoftPOS
        ↓
Payment confirmed
        ↓
Settlement process starts
```

The supplier must explicitly agree to release the order before customer payment. Nuvia's target is a short settlement window (approximately 30 minutes) after successful payment, subject to the actual PSP/banking capabilities and commercial agreement.

Nuvia should use an authorised payment provider for the regulated payment flow. It should not build its own wallet or informal escrow mechanism.

---

## Core Pilot Hypotheses

1. Customers value a plan-linked basket enough to reorder weekly.
2. Customers prefer seeing the package before paying and accept courier SoftPOS.
3. Suppliers will release small, approved orders before customer payment in exchange for a reliable short settlement cycle.
4. Planned routes create better courier economics than ad-hoc instant delivery.
5. Dietitians will adopt a free client-management/planning tool when it improves continuity and reduces execution friction.
6. Local supplier pricing can keep Phase 1 economics viable without owning inventory.
7. Atakum provides sufficient customer density for a controlled pilot.

Every hypothesis must be replaced by measured evidence during the pilot.

---

## Success Criteria for Phase 1

The pilot proceeds to Phase 2 only if the core evidence supports:

- meaningful week-1 → week-4 customer retention;
- at least 5 dietitians actively generating orders in the final month;
- non-negative contribution at the target customer density;
- acceptable quality/complaint rates;
- suppliers willing to continue the pre-payment release + short-settlement arrangement;
- customers accepting delivery-time SoftPOS payment.

A stop is a valid outcome. The pilot exists to answer the question cheaply.

---

## Guiding Principles

1. **Validate before building.**
2. **Adherence is the product.**
3. **The dietitian is a professional partner, not merely a sales channel.**
4. **The customer app owns the customer relationship.**
5. **Local first.**
6. **Predictability beats speed.**
7. **Do not over-engineer.**
8. **The dietitian owns clinical decisions; Nuvia owns execution.**

**The test for every feature:** does it help the weekly plan → basket → delivery → continuation loop? If not, it is probably out of scope.

---

## Project Status

**Stage:** Pre-pilot. Documentation foundation in progress.

**No application code has been written.** The immediate work is validation: partner interviews, real supplier pricing, courier economics, payment-provider feasibility and customer price testing.

### Immediate next actions

- [ ] Build Atakum dietitian target list
- [ ] Book dietitian conversations
- [ ] Price 5 real nutrition plans with local suppliers
- [ ] Interview couriers and validate planned-route rates
- [ ] Price-test the weekly package with potential customers
- [ ] Validate SoftPOS + settlement capabilities with Turkish PSPs
- [ ] Confirm regulatory/KVKK position with a local advisor
- [ ] Hold go/no-go review before MVP build

---

*When the docs and reality disagree, update the docs.*
