# Business Model

> Phase 1 model: **partner-based nutrition logistics.** We own the coordination layer and the customer relationship. We do not own inventory, vehicles, or production.

---

## 1. Model in One Paragraph

A dietitian creates a nutrition plan for their client inside our platform. The system converts that plan into a **weekly shopping basket** with exact products and quantities. The customer reviews and approves it in the app. We route the basket to local suppliers (butcher, chicken supplier, greengrocer, market), consolidate it, and hand it to an independent courier who delivers it on a planned route at a scheduled time window. The customer pays a weekly subscription price. We keep a margin, the dietitian earns a commission (~5%), the supplier gets predictable volume, and the courier gets predictable paid work.

**We are an orchestration business.** Our asset is demand we can see a week in advance.

---

## 2. Participants

### 2.1 Customers

**Who:** People in Atakum already paying a dietitian, or gym members buying a transformation package, who have decided to change how they eat and are failing at the execution step.

**What they receive:**
- Personalised weekly food supply, derived from their own dietitian's plan
- Correct products in correct quantities — no portion guesswork, minimal waste
- Dietitian-approved basket, so every item is "allowed"
- Subscription-based ordering: approve, do not decide
- Scheduled delivery in a known window, not a random arrival
- Progress tracking visible to both them and their dietitian

**What they pay:** 1,500–2,000 TL per weekly package (see [`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md)).

**Why they stay:**
- The cognitive load of eating properly drops close to zero
- Their dietitian can see adherence, so guidance improves
- Planned buying is often *cheaper* than their previous reactive shopping plus food waste
- Visible results

**Why they leave (design against this):** price shock, a bad delivery, quality inconsistency, or losing their dietitian relationship. All four are addressed in [`RISKS_AND_MITIGATION.md`](./RISKS_AND_MITIGATION.md).

---

### 2.2 Dietitians

**Who:** Independent dietitians and small clinics in Atakum. Typically solo practitioners running Instagram-led acquisition, seeing 20–80 clients, and losing most of them within 4–8 weeks.

**What they do on the platform:**
- Add and manage their own clients
- Build nutrition plans (weekly meal structure + ingredient requirements)
- Generate the weekly order from the plan — one action, not a shopping list they have to write by hand
- See adherence: did the client accept the package, did they receive it, did they log progress
- Track retention and commission

**What they earn:** ~5% commission on every completed order from their clients.

**Why the commission is deliberately secondary:** if a dietitian's primary motivation is commission, they become a salesperson, plans get inflated to raise basket value, and trust collapses. The commission exists to make the platform *non-costly* to them, not to make it a revenue business. The real pitch is in [`PARTNER_ACQUISITION.md`](./PARTNER_ACQUISITION.md):

> **"We help your clients follow your plans more consistently."**

**What they actually gain:**
- **Retention.** A client who eats to plan sees results and keeps paying for consultations. Extending average client life from 6 weeks to 12 weeks roughly doubles the practice's revenue with zero extra acquisition.
- **Better outcomes → better reputation → referrals.** Their marketing problem partially solves itself.
- **Professional differentiation.** "My clients get their food supplied" is a strong competitive claim against other local dietitians.
- **Time saved.** No more answering "which brand of yoghurt", "how much is 150g of chicken", "can I substitute this".
- **Adherence data.** They stop guessing whether a client followed the plan.

**Constraints we impose on ourselves:** we never contact a dietitian's client to sell them a different dietitian, and we never use plan content commercially. This is stated in the partner agreement.

---

### 2.3 Fitness Centres

**Who:** Gyms, CrossFit boxes, personal training studios, and pilates/functional studios in Atakum.

**Role:** Primarily a **customer acquisition channel**, secondarily a credibility signal.

**What they do:**
- Offer nutrition supply as a component of transformation / body-composition packages
- Refer members to partner dietitians on the platform
- Optionally host a partner dietitian on-site (a chair one day a week costs the gym nothing and closes deals)

**What they gain:**
- They can finally promise a *complete* transformation product instead of training alone
- Higher-priced package tiers ("Training + Nutrition + Supply")
- Better member results → better member retention, which is a gym's core economic problem
- Referral fee or revenue share on referred customers (structure agreed per partner; a per-active-customer monthly fee is simplest to administer)

**Pitch:** *"Transform your membership into a complete lifestyle program."*

---

### 2.4 Local Suppliers

**Who:**
- Butchers / meat shops (red meat, portioned)
- Chicken suppliers (breast, whole, portioned)
- Greengrocers and local markets (vegetables, fruit, staples)
- Local food businesses (dairy, eggs, bulgur/legumes, dried goods, local producers)

**What they do:** receive a consolidated weekly order list, prepare and portion it against our spec, and hold it for courier pickup at a scheduled time.

**What they gain:**
- **Predictable, forecastable volume.** They see the week's aggregate order in advance — this is unusually valuable in a business run on daily guesswork.
- **No customer acquisition cost.** We bring the demand.
- **Batch preparation.** Preparing 60 portions of chicken breast at once is far more efficient than 60 walk-in customers.
- **Prompt, consolidated payment.** One invoice, one payer, agreed terms.

**What we require:**
- Portion accuracy within a tolerance we specify
- Cold-chain handling and hygiene standards
- A named contact and a hard pickup-ready time
- Consistent, agreed pricing for the term

**Deliberate constraint:** start with a *small* number of suppliers (2–4 total) — quality control beats catalogue breadth in Phase 1.

---

### 2.5 Couriers

**Who:** Independent motorcycle and small-vehicle couriers in Atakum; existing delivery workers seeking supplementary income; local courier communities.

**Model:** independent contractors paid per planned route, not per drop.

**What they get before starting work:**
- The full delivery list
- The optimised route
- Every address and time window
- Expected total duration and total pay

**Why this is strictly better than instant delivery work:**

| | Instant delivery | Planned route |
|---|---|---|
| Idle waiting | High, unpaid | None — the route is known |
| Income predictability | Per-drop, variable | Fixed per route, known in advance |
| Route efficiency | Random dispatch, backtracking | Clustered, optimised, dense |
| Schedule control | Always-on availability | Chosen shifts, fixed days |
| Cognitive load | Constant dispatch pressure | One list, one route |

**We explicitly do not compete with Getir-style instant delivery.** We are not bidding for the same labour on the same terms; we are offering a different, calmer product to the same labour pool. See [`PARTNER_ACQUISITION.md`](./PARTNER_ACQUISITION.md).

---

## 3. The Win-Win Structure

Every participant's incentive must point toward the same outcome: **the customer keeps eating to plan, week after week.**

```
                    ┌─────────────────────────────┐
                    │   CUSTOMER ADHERENCE        │
                    │  (weeks of continuous plan  │
                    │        compliance)          │
                    └──────────────┬──────────────┘
                                   │
        ┌──────────────┬───────────┼───────────┬──────────────┐
        │              │           │           │              │
   ┌────▼────┐   ┌─────▼─────┐ ┌───▼────┐ ┌────▼─────┐  ┌─────▼─────┐
   │CUSTOMER │   │DIETITIAN  │ │FITNESS │ │SUPPLIER  │  │  COURIER  │
   │         │   │           │ │CENTRE  │ │          │  │           │
   │ results │   │ retention │ │ member │ │ stable   │  │ dense,    │
   │ + less  │   │ + referral│ │ results│ │ weekly   │  │ predictable│
   │ effort  │   │ + commis. │ │ + tier │ │ volume   │  │ routes    │
   └─────────┘   └───────────┘ └────────┘ └──────────┘  └───────────┘
        │              │           │           │              │
        └──────────────┴───────────┼───────────┴──────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │        PLATFORM             │
                    │  subscription margin +      │
                    │  forecastable demand +      │
                    │  route density              │
                    └─────────────────────────────┘
```

**Alignment check, participant by participant:**

| Participant | Gains when adherence is high | Loses when adherence is low |
|---|---|---|
| Customer | Results, time saved, less waste | Wasted money, lost confidence |
| Dietitian | Longer client life, referrals, commission | Churned client, damaged reputation |
| Fitness centre | Member results, higher-tier packages | Member churn |
| Supplier | Stable recurring volume | Volatile, unforecastable orders |
| Courier | Dense routes, predictable income | Sparse routes, low pay per hour |
| Platform | Recurring revenue, route density, margin | CAC burn with no LTV |

**No participant profits from a customer who quits.** That is the test of the model, and it is the reason the commission to dietitians is small and the emphasis on retention is large. A model where the dietitian earns most from basket size would break this alignment immediately.

---

## 4. Revenue Streams

**Phase 1 (active):**
1. **Margin on the weekly package.** Retail package price minus food cost. This is the only meaningful stream in Phase 1 and it is intentionally thin.
2. **Delivery contribution.** Bundled into the package price; not billed separately, to keep the price legible.

**Phase 2 (planned):**
3. **Bulk purchasing spread.** Buying at wholesale into a micro-fulfilment centre rather than at supplier retail.
4. **Fitness centre B2B packages.** Contracted volume sold to a gym rather than individual.

**Phase 3 (planned):**
5. **Prepared meal margin.** Structurally higher than raw ingredient margin.
6. **Product lines.** Performance nutrition, supplements, meal add-ons.

**Deliberately not in Phase 1:**
- SaaS fees charged to dietitians — this would kill partner acquisition, which is the hardest part of Phase 1. The dietitian dashboard is free, permanently, for partners who generate orders.
- Advertising or supplier listing fees — this corrupts quality control.
- Marketplace commissions on non-plan items — this makes us a grocery store.

---

## 5. Cost Structure (Phase 1)

| Cost | Type | Notes |
|---|---|---|
| Food cost (supplier) | Variable | Largest line by far, ~70% of package |
| Courier payment | Variable per route | Falls per-customer as density rises |
| Dietitian commission (~5%) | Variable | Paid only on completed orders |
| Payment processing | Variable | Turkish PSP rates + per-transaction fee |
| Packaging / cold chain | Variable | Insulated bags amortised; consumables per order |
| Operations staff | Fixed | Part-time coordinator in Phase 1 |
| Software / infrastructure | Fixed | Small; see MVP requirements |
| Partner acquisition | Fixed-ish | Founder time, minimal spend |

Detailed numbers: [`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md).

---

## 6. What Makes This Defensible

Order matters — these compound in sequence:

1. **The dietitian network.** A competitor must convince the same professionals to switch, against an existing working relationship and their clients' habits. This is slow, human, local work that capital cannot compress.
2. **Route density.** Delivery economics improve superlinearly with customers per route. The first operator to reach density in a district is structurally cheaper than the second.
3. **Supplier relationships.** Reliable local suppliers with agreed portioning and pricing are a scarce, relationship-bound resource in a mid-size city.
4. **Plan → basket data.** Every plan converted into a basket improves our mapping between nutritional requirements and real, locally available products. This is a genuine data asset and it is the foundation of Phase 3.
5. **Switching cost via outcomes.** A customer 10 weeks into visible progress does not experiment with an alternative supplier.

Note what is *not* on this list: technology, speed, and capital. None of them are our moat in Phase 1, and building as if they were is the main way this project fails.

---

## 7. Key Business Assumptions to Validate

These are the beliefs the whole model rests on. [`VALIDATION_PLAN.md`](./VALIDATION_PLAN.md) is designed to test them.

| # | Assumption | How Phase 1 tests it | Kill signal |
|---|---|---|---|
| A1 | Customers will reorder a plan-linked weekly package | Week-over-week reorder rate | <30% reach week 4 |
| A2 | Dietitians will actively use the dashboard unprompted | Orders generated per dietitian per month | Median <2 after week 6 |
| A3 | Planned delivery cost per drop is workable at low density | Measured cost per delivery | >200 TL/drop at 40+ customers |
| A4 | Local suppliers can hold quality and portioning | Complaint rate per delivery | >5% of deliveries |
| A5 | Price is acceptable to the Atakum segment | Conversion from dietitian referral to paying customer | <20% conversion |
| A6 | Couriers prefer planned routes | Courier retention across the pilot | Losing >1 of 3 couriers |
