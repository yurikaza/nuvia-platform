# Validation Plan — 8-Week Atakum Pilot

> The pilot is an experiment, not a launch. Its output is **evidence**, not revenue.
>
> **The single question:** will customers, unprompted, approve and pay for a second, third, fourth, and eighth weekly package?

---

## 1. Structure

| Weeks | Phase | Objective |
|---|---|---|
| **1–2** | Discovery | Interview partners, discover suppliers, interview couriers. Correct or kill the assumptions before building anything. |
| **3–4** | Build & Sign | Build the MVP. Sign the first dietitians, suppliers, couriers, gyms. |
| **5–8** | Run | Operate the pilot. Measure. Talk to everyone, every week. |

**Budget for the pilot:** roughly 40,000 TL/month in fixed costs plus an expected 10,000–25,000 TL/month operating loss ([`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) §5–6). Plan for ~150,000 TL total over the eight weeks. Founder time is unpaid.

---

# Weeks 1–2: Discovery

**No code is written in these two weeks.** The purpose is to find out whether the assumptions in [`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) §10 survive contact with Atakum.

## Partner Interviews (Dietitians)

**Target: 20+ conversations, 10 in-person.**

Build the target list from Google Maps and Instagram ([`PARTNER_ACQUISITION.md`](./PARTNER_ACQUISITION.md) §1). Ask for their opinion, not their signature.

**Questions that matter:**
1. How many clients do you have now? How many were with you three months ago?
2. When a client stops, why do they stop? *(Listen for adherence vs. price vs. results.)*
3. What percentage of your clients actually follow the plan you write?
4. How do you know whether they followed it?
5. What do clients ask you between sessions? *(Portion and product questions = our thesis confirmed.)*
6. How do you write plans today? How long does one take?
7. If your clients' food arrived pre-portioned and matched to your plan, what changes for you?
8. What would make you refuse to use a tool like this?
9. Would you introduce this to 3–5 clients as a trial?

**What we are testing:** whether adherence is genuinely their top churn driver, whether they will invite clients, and whether the plan-entry workflow is feasible for them.

**Deliverables:** interview notes, a ranked prospect list, a documented plan-creation workflow observed from at least 3 dietitians, and 5+ verbal commitments to trial.

## Supplier Discovery

**Target: visit 8–10, shortlist 4, sign 2–4.**

Butchers, chicken suppliers, greengrocers, dairy and dry goods in Atakum.

**What to establish:** willingness to portion to spec and at what tolerance; wholesale-ish pricing at weekly volume; pickup-ready time feasibility for a Sunday morning; hygiene and cold-chain practice; capacity headroom; and who the actual named contact is.

**Critical output — price 5 real baskets.** Take five actual nutrition plans from the dietitian interviews and price them with real suppliers. This is the only way to validate **Assumption A (food cost = 70% of package price)**, and that assumption determines whether the model has any margin at all.

**Deliverables:** shortlist with prices, 5 priced real baskets, validated (or corrected) food cost ratio, draft supplier terms.

## Courier Interviews

**Target: 6–8 conversations.**

Independent motorcycle couriers, existing delivery workers, local courier communities.

**Questions:** what do you earn on a typical day and how much of it is waiting? What do you dislike most about instant-delivery work? If you knew the whole route and the total pay before you started, what would make that worth taking? What is a fair shift guarantee? Would you commit to a fixed Sunday shift?

**What we are testing: Assumption B (700 TL + 50 TL/stop).** This number is low-confidence and directly determines delivery economics. It should be corrected by these conversations, not defended.

**Deliverables:** validated courier rate, 3 candidates identified, confirmed availability on the planned delivery day.

## Additional Week 1–2 Work

- **Customer price testing.** Talk to 10–15 potential customers (dietitian clients, gym members). Ask what they currently spend weekly on food, what they waste, and how they react to 1,500 / 1,750 / 2,000 TL. Tests **Assumption H**.
- **Fitness centre visits.** 5–6 gyms; establish interest and referral structure.
- **Address mapping.** Ask interviewed dietitians roughly where their clients live. Early evidence on **Assumption J (route density)**.
- **Legal check.** Confirm the Phase 1 regulatory position and KVKK obligations with a local advisor.
- **PSP quotes.** iyzico and PayTR rates, settlement terms, onboarding time. Tests **Assumption C**.

## Week 2 Go/No-Go

Do not proceed to build unless:

| Gate | Threshold |
|---|---|
| Dietitians verbally committed to trial | ≥5 |
| Suppliers willing to portion at workable prices | ≥2 |
| Food cost ratio on real baskets | ≤75% of target price |
| Couriers available at a workable rate | ≥3 |
| Customer price reaction | Not overwhelmingly negative |

**If food cost comes back at 85%, stop.** The model has no margin and no amount of software fixes it. Re-plan the pricing or the sourcing before writing a line of code.

---

# Weeks 3–4: Build & Sign

Two tracks in parallel: one person builds, one person signs. If there is only one person, signing wins and the MVP scope shrinks.

## Build the MVP

Two weeks, following the build order in [`MVP_TECHNICAL_REQUIREMENTS.md`](./MVP_TECHNICAL_REQUIREMENTS.md) §6.

| Days | Deliverable |
|---|---|
| 1–2 | Auth, roles, ops records for customers/suppliers/couriers |
| 3–4 | Product catalogue and pricing |
| 5–7 | Dietitian: clients, plan templates, plan creation |
| 8–9 | Basket generation from plan — tested against the 5 real baskets from week 2 |
| 10–11 | Customer: registration, profile, basket approval |
| 12 | Payment integration |
| 13 | Supplier pick-list aggregation; ops metrics page |
| 14 | Route building, courier interface, notifications, end-to-end test |

**Minimum viable for week 5:** steps 1–8. Route dispatch by WhatsApp is acceptable if the courier interface is not ready.

**Mandatory before the first real order:** run one complete fake order end to end — plan → basket → approval → test payment → pick list → route → delivery confirmation — with the founding team playing every role.

## Sign the Partners

| Target | Count |
|---|---|
| Dietitians signed | 5–10 |
| Dietitians onboarded in person with their own templates built | all signed |
| Suppliers signed with written terms | 2–4 |
| Couriers onboarded | 3 |
| Fitness centres signed | 1–2 |
| Customers invited by dietitians | 30–50 invitations |

**Onboarding a dietitian means sitting with them and building their templates.** An account created and abandoned is not an onboarded partner — this is Risk 5 and it is the most likely quiet failure of the pilot.

## Week 4 Go/No-Go

| Gate | Threshold |
|---|---|
| MVP handles the loop end to end | Yes |
| Dietitians signed and onboarded | ≥5 |
| Suppliers signed | ≥2 |
| Couriers onboarded | ≥2 |
| Customers registered | ≥15 |
| Test order completed successfully | Yes |

Fewer than 15 registered customers means the dietitian channel is not converting. Fix the invitation flow and the dietitian pitch before starting week 5 — a pilot with 8 customers produces no usable retention data.

---

# Weeks 5–8: Run the Pilot

Four full weekly cycles. This is the minimum needed to observe a week-4 retention number for the first cohort.

## The Weekly Rhythm

Full detail in [`OPERATIONS.md`](./OPERATIONS.md) §2. Every week, without exception:

- **Thursday:** baskets generated, dietitians confirm, customers notified
- **Friday:** approval cutoff 18:00, pick lists to suppliers
- **Saturday:** routes built and published to couriers
- **Sunday:** delivery window 10:00–16:00
- **Monday:** reconcile, handle complaints, pay couriers
- **Tuesday:** **metrics review and risk register review** — the most important hour of the week

## Week-by-Week Focus

**Week 5 — Does it work at all?**
Target 15–30 customers. Founders run a delivery route personally. Expect operational failures; the point is to find them. Call every single customer after the first delivery — every one, without exception. This is the highest-information day of the entire pilot.

**Week 6 — Does anyone come back?**
Target 30–50 customers. **The first reorder data arrives.** Watch approval rate before cutoff and the first skips. Week-2 check-in with every dietitian — this is when silent partner drop-off happens. Fix the top 3 operational failures from week 5.

**Week 7 — Does it hold?**
Target 40–70 customers. Watch route density and cost per delivery as customer count grows. Week-3 retention for the first cohort. Structured interviews with 5 customers and 3 dietitians. Begin second-cohort acquisition through fitness centres.

**Week 8 — What did we learn?**
Target 50–100 customers. **Week-4 retention for the first cohort — the headline number.** Full metrics review, structured exit interviews with every churned customer, and the go/no-go decision for Phase 2.

## Continuous Activities

- Talk to 3+ customers every week, by phone, not survey
- Check in with every active dietitian weekly
- Ride along on a route at least once per week
- Log every operational failure with a root cause
- Update the assumption register ([`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md) §10) as real data replaces estimates
- Review the risk register every Tuesday
- Keep recruiting dietitians — the funnel never stops

---

# Success Criteria

## Primary — the four things that decide Phase 2

### 1. Customers reorder

The core hypothesis. Nothing else matters if this fails.

| Metric | Success | Marginal | Fail |
|---|---|---|---|
| Week-4 retention (cohort 1) | ≥40% | 30–40% | <30% |
| Week-8 retention (cohort 1) | ≥25% | 15–25% | <15% |
| Weekly repeat order rate | ≥70% | 50–70% | <50% |
| Skip rate | ≤15% | 15–25% | >25% |

### 2. Dietitians continue using the system

| Metric | Success | Marginal | Fail |
|---|---|---|---|
| Active dietitians in the final month | ≥5 | 3–4 | <3 |
| Orders per active dietitian per month | ≥8 | 4–8 | <4 |
| Client activation rate (invited → paying) | ≥30% | 15–30% | <15% |
| Dietitians who would recommend it to a peer | ≥80% | 60–80% | <60% |

### 3. Delivery economics work

| Metric | Success | Marginal | Fail |
|---|---|---|---|
| Cost per delivery | ≤130 TL | 130–180 TL | >200 TL |
| Stops per route | ≥12 | 8–12 | <8 |
| Contribution margin per order | ≥150 TL | 0–150 TL | <0 |
| On-time delivery rate | ≥90% | 80–90% | <80% |
| Failed delivery rate | ≤3% | 3–7% | >7% |

### 4. Customer feedback is positive

| Metric | Success | Marginal | Fail |
|---|---|---|---|
| Quality complaint rate | <3% | 3–7% | >10% |
| Would recommend to a friend | ≥70% | 50–70% | <50% |
| "Saves me time and effort" agreement | ≥80% | 60–80% | <60% |
| Reported adherence improvement | ≥60% | 40–60% | <40% |

## Secondary

| Metric | Target |
|---|---|
| Active customers at week 8 | 50–100 |
| Average order value | 1,600–1,900 TL |
| Food cost ratio | ≤72% |
| Payment failure rate | ≤3% |
| Courier retention | ≥2 of 3 |
| Monthly burn | ≤30,000 TL |
| Fitness centre referrals | ≥10 customers |

---

# Qualitative Evidence

Numbers at 50–100 customers are directionally useful but statistically thin. The qualitative work is not optional.

**Every churned customer gets an exit interview.** One question above all others: *why did you stop?* Categorise: price, quality, delivery, results, plan fit, life circumstances, lost their dietitian. This distribution is the most decision-relevant output of the entire pilot.

**Structured week-8 interviews:**
- **10 active customers** — what would make you stop? What is worth the money? What is missing? Are you eating better than before?
- **All active dietitians** — has this changed your client retention? Is the tool faster than your old method? Would you recommend it? What would make you stop?
- **All couriers** — is this better than instant delivery work? Is the pay fair? Would you continue?
- **All suppliers** — is the volume useful? Is the process workable? Can you handle 3× this?

---

# Decision Framework — End of Week 8

| Outcome | Condition | Action |
|---|---|---|
| **Proceed to Phase 2** | All 4 primary criteria at Success | Begin micro fulfilment centre planning; scale to 250 customers first |
| **Extend the pilot** | 3 of 4 at Success, 1 marginal | Run 8 more weeks, fix the weak dimension, re-decide |
| **Pivot** | Retention succeeds, economics fail | The demand is real, the delivery model is not. Test pickup points, fewer delivery days, or higher-value baskets. |
| **Pivot** | Economics succeed, dietitian channel fails | The logistics work, the channel does not. Test direct-to-consumer with an in-house dietitian. |
| **Stop** | Week-4 retention <30% and exit interviews show no product-market fit | The core hypothesis is false. Stop and write up what was learned. |

**A stop is a valid outcome.** The pilot is designed to cost ~150,000 TL and 8 weeks to answer a question that would otherwise cost years. Answering it "no" cheaply is a successful pilot.

---

# Reporting

- **Weekly** (Tuesday): one-page metrics snapshot, operational failures with root causes, assumption register updates, risk register review
- **Week 4:** build and signing gate review
- **Week 8:** full pilot report — every metric against target, the assumption register with measured values, all interview findings, the churn-reason distribution, and the Phase 2 recommendation

The week-8 report is the artefact this entire plan exists to produce.
