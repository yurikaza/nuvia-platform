# Nutrition Lifestyle Network

> **Working title.** A localized nutrition logistics platform connecting dietitians, fitness centres, customers, local suppliers, and delivery partners.
>
> **Pilot location:** Atakum, Samsun, Turkey.

---

## Positioning

> ### We are not a fast delivery company. We are a planned nutrition logistics network.

This sentence is the constraint on every product, operational, and hiring decision that follows. Speed is not our product. Consistency is.

---

## What This Is

People do not fail at healthy eating because they lack a plan. They fail in the gap between the plan and the plate — the shopping, the portioning, the daily decisions. Within three weeks the effort collapses, the results stall, the dietitian loses a client, and the customer concludes that "diets do not work for me."

**Nobody owns that gap.** It looks like a healthcare problem. It is a logistics problem.

We build the infrastructure that closes it:

```
Professional guidance  ──┐
Personalized plans     ──┤
Automated supply       ──┼──►  A habit that survives past week three
Planned delivery       ──┤
Long-term formation    ──┘
```

A dietitian writes a plan. The system turns it into a weekly basket. The customer approves rather than decides. Local suppliers prepare and portion it. An independent courier delivers it on a planned route at a known time. The customer eats to plan, sees results, and keeps going — and the dietitian, the gym, the supplier, and the courier all do better because of it.

---

## Why Atakum

| Reason | Detail |
|---|---|
| **Income distribution** | The strongest income profile in the Samsun metropolitan area — a 1,500–2,000 TL weekly food budget is achievable, not aspirational |
| **University population** | Ondokuz Mayıs University drives a young, health-literate, digitally native base plus academic households |
| **Active fitness culture** | Dense concentration of gyms, trainers, and independent dietitians already selling transformation |
| **Right size for a pilot** | Compact residential density makes planned multi-stop routes viable at low customer counts — the whole delivery economics argument depends on this |

---

## The Participants

| Participant | Gives | Gets |
|---|---|---|
| **Customer** | Weekly subscription | Personalized supply, plan-matched portions, near-zero decision load, visible results |
| **Dietitian** | Plans and clients | Client retention, better outcomes, adherence data, ~5% commission |
| **Fitness centre** | Member referrals | A complete transformation product, member results, higher-tier packages |
| **Local supplier** | Prepared, portioned goods | Predictable weekly volume, zero acquisition cost, one prompt payer |
| **Courier** | Planned route delivery | Known route, known pay, no idle waiting — before the shift starts |
| **Platform** | Coordination | Recurring revenue, forecastable demand, route density |

**No participant profits from a customer who quits.** That alignment is the model.

---

## Roadmap at a Glance

| Phase | Horizon | Question it answers | Model |
|---|---|---|---|
| **1 — Atakum Pilot** | Months 0–6 | Will customers reorder a plan-linked package? | Supplier + courier network |
| **2 — Micro Fulfilment** | Months 6–18 | Can we control cost and quality at volume? | Centralised inventory |
| **3 — Nutrition Production** | Months 18–36 | Will customers buy prepared personalised meals? | Production company |
| **4 — Network Expansion** | Months 36+ | Does the playbook transfer? | Multi-city |

**Phase 1 targets:** 10 dietitian partners · 2–3 fitness centres · 50–100 active customers · 2–3 couriers · 2–4 suppliers · one district only.

**Phase 1 is not a profit phase.** It exists to produce one piece of evidence: that customers reorder.

---

## Documentation

The `/docs` directory is the source of truth for this project. Read in this order.

| # | Document | What it covers |
|---|---|---|
| 1 | **[PROJECT_OVERVIEW.md](./docs/PROJECT_OVERVIEW.md)** | Problem statement, market opportunity, vision, mission, why this is not grocery delivery, long-term roadmap |
| 2 | **[BUSINESS_MODEL.md](./docs/BUSINESS_MODEL.md)** | All five participants in detail, the win-win structure, revenue streams, defensibility, assumptions to validate |
| 3 | **[PRODUCT_ROADMAP.md](./docs/PRODUCT_ROADMAP.md)** | Phase 1 feature scope across all four surfaces; Phase 2 fulfilment centre; Phase 3 production company |
| 4 | **[UNIT_ECONOMICS.md](./docs/UNIT_ECONOMICS.md)** | Cost breakdown per package, route density economics, break-even, LTV/CAC, metric definitions, assumption register |
| 5 | **[PARTNER_ACQUISITION.md](./docs/PARTNER_ACQUISITION.md)** | How to find and sign dietitians, gyms, couriers, and suppliers — channels, pitches, onboarding, tracking |
| 6 | **[OPERATIONS.md](./docs/OPERATIONS.md)** | The weekly operating calendar, every workflow stage, supplier management, quality control, support |
| 7 | **[RISKS_AND_MITIGATION.md](./docs/RISKS_AND_MITIGATION.md)** | Twelve risks with mitigations, early-warning indicators, and kill signals |
| 8 | **[MVP_TECHNICAL_REQUIREMENTS.md](./docs/MVP_TECHNICAL_REQUIREMENTS.md)** | Architecture, stack, backend scope, data model, build order, sanctioned shortcuts, out-of-scope list |
| 9 | **[VALIDATION_PLAN.md](./docs/VALIDATION_PLAN.md)** | The 8-week pilot: discovery, build, run, success criteria, decision framework |

---

## Core Numbers

| | |
|---|---|
| Weekly package price | 1,500–2,000 TL |
| Phase 1 contribution margin | ~9.5% (deliberately thin) |
| Food cost | ~70% of package price |
| Cost per delivery | ~120 TL at 10 stops · ~97 TL at 15 stops |
| Break-even | ~55–75 active customers |
| Dietitian commission | ~5% of completed orders |
| Pilot duration | 8 weeks |
| Expected pilot cost | ~150,000 TL |

Full model and every assumption: [UNIT_ECONOMICS.md](./docs/UNIT_ECONOMICS.md).

---

## Success Criteria for Phase 1

The pilot proceeds to Phase 2 only if all four hold:

1. **Customers reorder** — ≥40% of week-1 customers still active at week 4
2. **Dietitians keep using it** — ≥5 actively generating orders in the final month
3. **Delivery economics work** — cost per delivery ≤130 TL, contribution ≥0
4. **Customer feedback is positive** — complaint rate <3%, ≥70% would recommend

A stop is a valid outcome. The pilot is designed to answer the question cheaply, in either direction.

---

## Guiding Principles

1. **Validate before building.** Every phase falsifies one specific assumption.
2. **Adherence is the product.** Revenue is a lagging indicator of adherence.
3. **The dietitian is a partner, not a sales channel.** If a feature makes their practice worse, we do not ship it.
4. **Local first.** Local suppliers, local couriers, local trust — a defensibility strategy, not sentiment.
5. **Do not over-engineer.** Software not needed to prove the pilot hypothesis is a liability.

**The test for every proposed feature:** does this increase the number of consecutive weeks a customer eats according to their plan? If not, it is out of scope.

---

## Project Status

**Stage:** Pre-pilot. Documentation foundation complete.

**No application code has been written.** The next step is Weeks 1–2 of [VALIDATION_PLAN.md](./docs/VALIDATION_PLAN.md) — partner interviews, supplier discovery, and courier interviews — which must correct the assumption register before the MVP build begins.

### Immediate next actions

- [ ] Build the Atakum dietitian target list (Google Maps + Instagram), 40+ entries
- [ ] Book 20 dietitian conversations
- [ ] Visit 8–10 potential suppliers; **price 5 real nutrition plans** — this validates or kills the margin assumption
- [ ] Interview 6–8 couriers; correct the 700 TL + 50 TL/stop rate assumption
- [ ] Price-test 1,500 / 1,750 / 2,000 TL with 10–15 potential customers
- [ ] Get PSP quotes (iyzico, PayTR)
- [ ] Confirm the Phase 1 regulatory and KVKK position with a local advisor
- [ ] Hold the Week 2 go/no-go review before writing any code

---

*This documentation is the source of truth for the project. When the docs and reality disagree, update the docs.*
