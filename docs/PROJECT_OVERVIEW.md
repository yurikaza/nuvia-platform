# Project Overview — Nutrition Lifestyle Network

> **Working title.** Pilot location: Atakum, Samsun, Turkey.
> **Positioning:** *We are not a fast delivery company. We are a planned nutrition logistics network.*

---

## 1. Problem Statement

People who decide to change their eating habits almost never fail because of a lack of information. They fail at the **execution layer** between the plan and the plate.

The failure chain looks like this:

1. A person pays a dietitian and receives a nutrition plan.
2. The plan requires specific ingredients, in specific quantities, on specific days.
3. Buying those ingredients means multiple shops, unpredictable stock, unfamiliar portioning, and repeated decision-making.
4. Within 2–3 weeks the shopping burden collapses. The person substitutes, skips, or improvises.
5. Results stall. The customer blames the plan, stops paying the dietitian, and returns to old habits.

Three parties lose:

- **The customer** loses money and confidence, and concludes that "diets do not work for me."
- **The dietitian** loses a client after 1–2 months, is judged on results they did not control, and spends most of their working hours re-acquiring clients instead of practising.
- **The fitness centre** sells a transformation outcome it cannot actually deliver, because ~70% of body-composition change is driven by food it has no influence over.

Existing services do not close this gap:

| Service type | What it solves | What it does not solve |
|---|---|---|
| Instant grocery delivery (Getir, Migros Hemen) | Speed and convenience for *unplanned* needs | The customer still decides what to buy; no plan linkage, no portioning, no adherence |
| Meal-kit boxes | Ingredients + recipe | Generic menus, no professional supervision, no dietitian in the loop |
| Diet catering / meal prep | Ready meals | Fixed menus, high price, no personalisation, no habit formation — the customer never learns to eat |
| Dietitian consulting | The plan itself | No supply, no logistics, no adherence enforcement |

**Nobody owns the space between the nutrition plan and the customer's kitchen.** That space is a logistics problem wearing a healthcare costume.

---

## 2. Market Opportunity

### 2.1 Why Atakum, Samsun

Atakum is the highest-quality controlled pilot environment available to us:

- **Income distribution.** Atakum has the strongest income profile in the Samsun metropolitan area — the population can absorb a 1,500–2,000 TL/week food budget without treating it as a luxury.
- **University population.** Ondokuz Mayıs University drives a young, health-literate, digitally native cohort, plus academic staff households with disposable income.
- **Active fitness culture.** A dense concentration of gyms, personal trainers, and independent dietitians who already sell "transformation" packages.
- **Geographic compactness.** Atakum's residential density along the coastal axis makes planned multi-stop delivery routes economically viable at low customer counts — a route can be profitable at 8–12 stops.
- **Underserved by national players.** National instant-delivery operators treat Samsun as a secondary market; there is no local competitor offering plan-linked supply.

### 2.2 Market Layers

**Layer 1 — Direct pilot market (Atakum).** Active dietitian clients + gym members with transformation goals. A conservative estimate of the reachable base: 40–60 independent dietitians, 25+ fitness facilities, and several thousand people paying for structured nutrition guidance at any given time.

**Layer 2 — Samsun metropolitan expansion.** İlkadım, Canik, Tekkeköy. Same operating model, same suppliers, incremental route density.

**Layer 3 — Anatolian mid-size cities.** The model is deliberately designed for cities that national instant-delivery economics do not serve well: 300k–1M population, compact residential cores, strong local supplier networks. This is a large and structurally ignored market.

**Layer 4 — Personalised nutrition production.** Once demand is proven, the same customer relationship supports prepared meals, supplements, and performance nutrition at far higher margin (see Phase 3).

### 2.3 Why Now

- Health and body-composition awareness in Turkey has grown sharply, and dietitian consultation has normalised as a paid professional service.
- Independent dietitians increasingly operate as solo digital businesses (Instagram-led acquisition) and are acutely exposed to churn.
- Food inflation has made *planned* purchasing measurably cheaper than reactive purchasing — a planned weekly basket is a cost-saving argument, not only a convenience argument.
- Courier labour is abundant but poorly utilised: instant delivery pays per drop with unpredictable idle time. Planned routes are strictly better for the courier.

---

## 3. Vision

**A city where following a nutrition plan is the path of least resistance.**

We want the moment of "I will eat properly this year" to be followed by an infrastructure that makes the decision self-executing: the plan exists, the food arrives, the professional sees the adherence data, and the habit survives past the third week — the point where nearly every attempt currently dies.

Long term, we intend to be the layer that any nutrition professional in Turkey plugs into in order to make their plans physically real for their clients.

---

## 4. Mission

Build the operational infrastructure — software, supplier network, and planned delivery — that connects **dietitians, fitness centres, customers, local suppliers, and couriers** into a single loop where:

- the professional's plan becomes an automatically generated weekly order,
- the customer approves rather than decides,
- local suppliers get predictable, forecastable demand,
- couriers get planned, route-optimised, predictable work,
- and every participant's incentive points toward the customer's long-term adherence.

---

## 5. Why This Is Not Grocery Delivery

This distinction is the core of the company and must survive every product decision.

| Dimension | Instant grocery delivery | Nutrition Lifestyle Network |
|---|---|---|
| **Demand origin** | Customer impulse, unpredictable | Dietitian plan, generated by the system |
| **Time horizon** | 10 minutes | 7 days, known in advance |
| **Order composition** | Whatever the customer picks | Plan-derived basket, portioned to the person |
| **Delivery model** | On-demand, idle-heavy, one-drop routes | Scheduled, batched, optimised multi-stop routes |
| **Cost structure** | High cost per drop, dark-store capital | Low cost per drop via density and planning |
| **Competitive moat** | Speed and capital | Professional network + plan data + route density |
| **Customer relationship** | Transactional, zero switching cost | Subscription tied to a professional relationship and visible progress |
| **Success metric** | Orders per hour | Weeks of continuous adherence |
| **What we sell** | Convenience | Outcomes and consistency |

Three structural consequences:

1. **We know demand before it happens.** Because orders are generated from plans on a weekly cadence, we can forecast supplier volume days ahead. Instant delivery cannot. This is the source of our margin, not delivery speed.
2. **We do not compete on speed, so we do not need capital to win.** No dark stores in Phase 1, no 10-minute promise, no fleet on standby.
3. **Our churn driver is different.** Grocery delivery churns on price and speed. We churn on *results*. That makes the dietitian relationship the retention engine — and it is a relationship we strengthen rather than disintermediate.

> **The one-line test for every future feature:** does this increase the number of consecutive weeks a customer eats according to their plan? If not, it is out of scope.

---

## 6. Long-Term Roadmap

Detailed phase content lives in [`PRODUCT_ROADMAP.md`](./PRODUCT_ROADMAP.md). Summary:

### Phase 1 — Atakum Pilot *(Months 0–6)*
Partner-based nutrition logistics. Local suppliers prepare, independent couriers deliver on planned routes, software coordinates. Goal: prove that customers reorder and that per-delivery economics are workable. Not a profit phase.

**Exit criteria:** ≥40% of pilot customers complete 4+ consecutive weeks; ≥5 dietitians actively generating orders monthly; contribution margin per delivery ≥ 0.

### Phase 2 — Micro Fulfilment Centre *(Months 6–18)*
A single small facility in Atakum holds inventory, does bulk purchasing, portioning, and quality control. Suppliers become wholesale inputs rather than order-by-order fulfillers.

**Exit criteria:** COGS reduction ≥15% vs Phase 1; quality complaint rate <2% of deliveries; capacity to serve 500+ weekly packages.

### Phase 3 — Nutrition Production Company *(Months 18–36)*
From raw ingredients to prepared, personalised meals. Weight-loss, muscle-gain, and performance nutrition lines produced against known, plan-derived demand. Positioning is a **personalised nutrition company**, not catering.

**Exit criteria:** prepared-meal line at >35% gross margin; multi-district operation; repeatable city-launch playbook.

### Phase 4 — Network Expansion *(Months 36+)*
Replicate into Samsun districts, then comparable Anatolian cities. The transferable assets are the software, the dietitian-partnership playbook, and the route model — not the physical infrastructure, which is rebuilt locally in each city.

---

## 7. Guiding Principles

1. **Validate before building.** Every phase exists to falsify a specific assumption. Phase 1's assumption is *"customers will reorder a plan-linked food package."* Nothing else matters until that is answered.
2. **Adherence is the product.** Revenue is a lagging indicator of adherence.
3. **The dietitian is a partner, not a sales channel.** If a feature makes their practice worse, we do not ship it.
4. **Local first.** Local suppliers, local couriers, local trust. This is a defensibility strategy, not sentiment.
5. **Do not over-engineer.** See [`MVP_TECHNICAL_REQUIREMENTS.md`](./MVP_TECHNICAL_REQUIREMENTS.md). Software that is not needed to prove the pilot hypothesis is a liability.

---

## 8. Related Documents

- [`BUSINESS_MODEL.md`](./BUSINESS_MODEL.md) — participants and the win-win structure
- [`PRODUCT_ROADMAP.md`](./PRODUCT_ROADMAP.md) — phased product and feature plan
- [`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) — financial model and metrics
- [`PARTNER_ACQUISITION.md`](./PARTNER_ACQUISITION.md) — how we recruit dietitians, gyms, couriers
- [`OPERATIONS.md`](./OPERATIONS.md) — Phase 1 operational workflow
- [`RISKS_AND_MITIGATION.md`](./RISKS_AND_MITIGATION.md) — risk register
- [`MVP_TECHNICAL_REQUIREMENTS.md`](./MVP_TECHNICAL_REQUIREMENTS.md) — first software version
- [`VALIDATION_PLAN.md`](./VALIDATION_PLAN.md) — the 8-week pilot plan
