# Risks and Mitigation

> Risk register for Phase 1. Each risk carries an early-warning indicator and a kill signal. A kill signal means the assumption underneath the business is wrong — stop and re-plan rather than push harder.

**Severity scale:** Critical = threatens the business model · High = threatens the pilot · Medium = threatens a metric · Low = manageable friction

---

## Risk Summary

| # | Risk | Severity | Likelihood | Owner |
|---|---|---|---|---|
| 1 | Customers may not accept higher pricing | Critical | High | Founder |
| 2 | Insufficient delivery density | High | High | Ops |
| 3 | Product quality inconsistency | Critical | Medium | Ops |
| 4 | Over-dependence on dietitians | Critical | High | Founder |
| 5 | Dietitians sign but never use the platform | High | High | Founder |
| 6 | Supplier failure or capacity limits | High | Medium | Ops |
| 7 | Courier churn / no-shows | Medium | Medium | Ops |
| 8 | Food inflation erodes margin mid-pilot | High | High | Founder |
| 9 | Regulatory and food-safety compliance | High | Low | Founder |
| 10 | Operational complexity outruns a manual process | Medium | Medium | Ops |
| 11 | A funded competitor copies the model | Medium | Low | Founder |
| 12 | Customer data and health-data handling | Medium | Low | Founder |

---

# Risk 1 — Customers may not accept higher pricing

**Severity: Critical · Likelihood: High**

A customer comparing 1,750 TL/week against their own supermarket shop may conclude they are paying a large premium for convenience. If the segment rejects the price, no operational excellence saves the model.

The comparison is also unfair in our favour and hard to explain: their supermarket shop is not portioned, not plan-matched, generates waste, and costs them hours. But "it feels expensive" beats arithmetic in a purchase decision.

### Mitigation

**Low initial margin.** Phase 1 runs at ~9.5% contribution ([`UNIT_ECONOMICS.md`](./UNIT_ECONOMICS.md)) — deliberately thin so price cannot be blamed for churn. We would rather learn that retention works at a low margin than learn nothing at a high one.

**Local supplier pricing.** Sourcing from local butchers, chicken suppliers and greengrocers rather than retail chains keeps input cost genuinely lower. Local pricing is also a *story* customers in Samsun respond to.

**Trust through dietitians.** Price resistance drops sharply when the recommendation comes from a professional the customer already pays and believes. The dietitian is not a salesperson — they are a credibility transfer.

**Payment transparency.** Show the full itemised basket with per-item prices, always. Never a single opaque "package price". A customer who can see what they are buying can verify the value themselves, and the transparency itself signals we are not hiding a markup.

**Reframe the comparison.** Position against *total* current spend: groceries + food waste + shopping time + the failed diet attempt they already paid a dietitian for. Many customers discover they spend more today.

**Price tiers.** Offer 1,500 / 1,750 / 2,000 TL bands mapped to plan intensity, so budget is a plan conversation with their dietitian rather than a rejection of us.

### Early warning
Referral-to-paying conversion below 20%; price mentioned unprompted in >30% of onboarding conversations; skip rate rising in weeks 3–4 (the point where the second and third charges land).

### Kill signal
<20% conversion from dietitian referral to paying customer, sustained across 4+ dietitians. **Response:** the pricing model or the target segment is wrong. Test a smaller partial-week package (3-day supply, ~800 TL) before concluding the model fails.

---

# Risk 2 — Insufficient delivery density

**Severity: High · Likelihood: High**

Delivery economics are entirely density-driven. At 5 stops per route the cost per delivery is 190 TL and contribution nearly vanishes; at 15 stops it is ~97 TL and contribution nearly doubles. Scattered customers are the single fastest way to make this business unprofitable.

### Mitigation

**Start only in Atakum, and hold the line.** A customer in İlkadım or Canik who wants to sign up must be declined during the pilot. This will feel wrong every time and must be done anyway. Maintain a waitlist by district — it doubles as expansion evidence.

**Build concentrated customer clusters.** Treat geography as an acquisition criterion, not an afterthought:
- Map every customer address; visualise clusters continuously
- Prioritise dietitians whose client base sits in already-dense areas
- Target gyms in dense residential zones — their members live nearby
- Referral incentives for neighbours and same-building customers
- Prioritise apartment complexes and sites: many deliveries, one stop location

**Consolidate delivery days.** One delivery day in Phase 1. Adding days before adding customers halves density.

**Set a route minimum.** Do not run a route below 8 stops; consolidate into the next slot or have ops deliver personally instead.

### Early warning
Average stops per route below 8 after week 6; customer addresses spread across more than 4 distinct clusters; cost per delivery above 160 TL.

### Kill signal
Cost per delivery above 200 TL at 40+ active customers. **Response:** the address distribution is unworkable. Consider pickup points (partner gyms as collection hubs) before abandoning the delivery model.

---

# Risk 3 — Product quality inconsistency

**Severity: Critical · Likelihood: Medium**

In Phase 1 we do not touch the food. Suppliers portion and prepare it, couriers transport it, and the customer blames *us* for every defect. A single bad delivery can end a subscription; a food-safety incident can end the company.

### Mitigation

**Start with a very limited supplier set.** 2–4 suppliers total. Every added supplier multiplies the quality surface. Catalogue breadth is worthless if the chicken is inconsistent.

**Build trusted local partnerships.** Choose suppliers on consistency, not price. Visit in person before signing. Place a sample order and inspect it. Meet the person who will actually do the portioning — in a local butcher shop, that relationship is the quality control system.

**Written specification per product.** Cut, fat ratio, portion weight and tolerance, freshness requirement, packaging, labelling. Ambiguity is where quality drifts.

**Multi-stage verification.** Courier verifies at pickup; ops spot-audits 2–3 random baskets per delivery day; customer rates post-delivery; ops reviews complaints by supplier weekly. Full detail in [`OPERATIONS.md`](./OPERATIONS.md) §5.

**Cold chain discipline.** Insulated bags, ice packs, chilled goods delivered within ~4 hours of pickup, chilled-heavy stops sequenced first.

**Resolve first, diagnose second.** Refund or replace on the first complaint without argument. The cost of a refund is trivial against the cost of a churned subscriber and a damaged dietitian relationship.

**Phase 2 is the structural fix.** Owning the fulfilment centre converts quality from a supplier promise into a process we run. This is the strongest argument for Phase 2 — stronger than the margin argument.

### Early warning
Complaint rate above 3%; repeat complaints on the same product; any temperature or freshness complaint; supplier missing a pickup-ready time.

### Kill signal
Complaint rate above 10% of deliveries, or any food-safety incident. **Response:** halt the affected product line immediately, replace the supplier, and do not resume until a sample audit passes.

---

# Risk 4 — Over-dependence on dietitians

**Severity: Critical · Likelihood: High**

Dietitians are our acquisition channel, our credibility, our retention mechanism, and our plan source. That concentration is dangerous in three directions:

- A dietitian who leaves may take their whole client list
- A dietitian who becomes a competitor already knows the model
- A dietitian relationship that sours can turn a segment of the local professional community against us

### Mitigation

**Build a direct customer relationship through the platform.** The customer's ongoing experience — the app, the delivery, the support, the reliability — must be ours, not the dietitian's. Specifically:
- Our brand on the app, packaging, and every courier interaction
- Our support handles all service issues directly
- Progress tracking, adherence streaks, and delivery history live with us
- Weekly touchpoints (approval, delivery) that are ours, not the dietitian's

**Make the customer's switching cost independent of the dietitian.** If a customer changes dietitian, their address, preferences, delivery history, progress data, and subscription persist. Changing professional should not mean restarting with us.

**Diversify the channel.** Fitness centres, direct sign-up, and word of mouth should all produce customers. Track channel mix explicitly and treat >70% from any single channel as a warning.

**Never depend on one dietitian.** Cap any single dietitian at ~25% of the active customer base during the pilot. If one partner approaches that share, prioritise recruiting others over growing them.

**Make the partnership genuinely good.** The most effective defence is that leaving costs them retention, tooling, and adherence data they cannot rebuild alone.

**Fair, written terms.** No exclusivity demanded, no client poaching, clear data boundaries, easy exit. A partner who feels trapped becomes a competitor; a partner who feels well-treated becomes a reference.

### Early warning
One dietitian above 30% of active customers; a dietitian asking detailed questions about supplier relationships and margins; any partner going quiet after previously being active.

### Kill signal
Losing a dietitian and >50% of their customers with them. **Response:** the direct relationship is not real. Halt growth and fix the customer-facing experience before recruiting more partners.

---

# Risk 5 — Dietitians sign but never use the platform

**Severity: High · Likelihood: High**

The most likely quiet failure. A dietitian agrees in a meeting, creates an account, adds two clients, finds plan entry slower than their existing Word document or WhatsApp habit, and never returns. Ten signed partners and one active partner is a failed pilot that looks like a successful one on paper.

### Mitigation

- **Onboard in person and build their own templates with them.** The tool must be faster than their current method within the first hour, or it never will be.
- **Template-first design.** Cloning and adjusting a saved plan must take under two minutes.
- **Start small.** 3–5 clients each, not their whole book.
- **Week-2 check-in.** This is when silent drop-off happens.
- **Week-4 retention review.** Show them their own client-retention numbers. This is the moment the value proposition becomes concrete.
- **Measure activation, not signatures.** The reported metric is *dietitians generating orders in the last 30 days*, never *dietitians signed*.

### Early warning
Median orders per dietitian below 2 after week 6; more than half of signed partners inactive; support questions revealing they are still writing plans outside the platform.

### Kill signal
Fewer than 3 active dietitians at week 8 despite 8+ signed. **Response:** the dashboard is not usable enough. Consider having ops enter plans on the dietitian's behalf as a service, and re-evaluate the tooling.

---

# Risk 6 — Supplier failure or capacity limits

**Severity: High · Likelihood: Medium**

A supplier misses a pickup time, cannot fulfil a volume spike, closes for a holiday, or raises prices mid-term. With 2–4 suppliers, any single failure hits a large share of orders.

### Mitigation

- Named backup supplier for every critical category, contacted quarterly even when unused
- Fixed-term pricing agreements with a review clause
- Volume forecasts shared a week ahead so capacity is never a surprise
- Written shortfall protocol: report by Saturday 12:00, substitute, notify affected customers **before** delivery day
- Turkish holiday calendar mapped against delivery days at the start of the pilot
- Prompt payment, always — being the customer a supplier prioritises is worth more than a negotiated discount

### Early warning
Any missed pickup-ready time; a supplier hesitating on a volume forecast; unrequested price changes.

---

# Risk 7 — Courier churn or no-shows

**Severity: Medium · Likelihood: Medium**

Couriers are contractors with other options. A no-show on delivery day affects every customer on that route simultaneously.

### Mitigation

- Recruit 3 for 2 routes — the third is planned redundancy, not overstaffing
- Guaranteed shift floor (700 TL) makes our shift the most reliable option they have
- Publish routes the day before so the shift is confirmed in advance
- Pay weekly, on time, without exception
- Ops runs the route personally if a courier does not appear. **The route always runs.**
- Treat couriers well and visibly — courier communities talk, and that channel recruits or repels

### Early warning
A courier declining shifts; a confirmation arriving late; complaints about route quality or pay.

---

# Risk 8 — Food inflation erodes margin mid-pilot

**Severity: High · Likelihood: High**

Turkish food inflation can move input costs materially inside an 8-week pilot. With ~9.5% contribution, a 10% food-cost increase wipes out the margin entirely.

### Mitigation

- Fixed-term supplier pricing (3 months) covering the pilot window
- Weekly food-cost-ratio tracking as a Tier 3 metric, not a quarterly review
- Plan-level flexibility: dietitians can substitute toward seasonal, cheaper protein and produce without changing nutritional targets
- **Do not raise prices during the pilot.** Absorb the margin hit; the retention signal is worth more than the margin. Re-baseline pricing after week 8.
- Model contribution at ±15% food cost so the downside is known in advance

### Early warning
Food cost ratio above 72%; any supplier requesting an early price review.

---

# Risk 9 — Regulatory and food-safety compliance

**Severity: High · Likelihood: Low (Phase 1) / High (Phase 2–3)**

Phase 1 exposure is limited — we transport supplier-prepared goods rather than producing food. Phase 2 (fulfilment centre) and Phase 3 (production kitchen) require full food-business licensing, hygiene certification, and HACCP-equivalent processes.

### Mitigation

- Confirm the Phase 1 legal position with a local advisor before the pilot starts — specifically whether consolidated transport of supplier-prepared food requires registration
- Verify every supplier holds valid food-business registration and hygiene certification; keep copies
- Courier hygiene training and health certificates where required
- Cold-chain records retained
- Begin Phase 2 licensing work early — permits are slower than fit-out
- Product liability insurance from Phase 2

---

# Risk 10 — Operational complexity outruns a manual process

**Severity: Medium · Likelihood: Medium**

The Phase 1 process is intentionally semi-manual. It works at 50–100 customers. It does not work at 250, and the failure mode is gradual degradation — late pick lists, routing errors, missed complaints — rather than an obvious break.

### Mitigation

- Cap pilot growth at 100 customers. Waitlist beyond that. Growth is not the Phase 1 objective.
- Track ops coordinator hours per week; above ~30 hours, automate the largest consumer
- Automate in observed order of pain, never in anticipation
- Treat the waitlist as evidence for Phase 2, not as lost revenue

---

# Risk 11 — A funded competitor copies the model

**Severity: Medium · Likelihood: Low**

An instant-delivery player or a national diet-catering company adds plan-linked supply.

### Mitigation

The model is not hard to describe and is hard to execute. Defensibility comes from things capital cannot buy quickly: the local dietitian network, route density in a specific district, supplier relationships in a mid-size city, and accumulated plan→basket mapping data. A national player entering Samsun would have to rebuild all four locally, and their instant-delivery cost structure actively works against planned logistics.

**Practical response:** move fast on dietitian relationships (the slowest asset to build), and be the incumbent partner before anyone else arrives.

---

# Risk 12 — Customer data and health-data handling

**Severity: Medium · Likelihood: Low**

We hold names, addresses, phone numbers, payment references, and health-adjacent data (weight, measurements, nutrition plans, allergies). Turkish KVKK obligations apply, and health-adjacent data warrants care regardless.

### Mitigation

- KVKK-compliant privacy notice and explicit consent at signup
- Store the minimum necessary; do not collect health data we have no use for
- No card data stored — PSP tokenisation only
- Access control: a dietitian sees only their own clients; couriers see only masked phone numbers and today's addresses
- Written data boundaries in the partner agreement: plan content is never used commercially, client lists are never shared between partners
- Confirm KVKK obligations with a local advisor before launch

---

## Review Cadence

This register is reviewed **weekly** during the pilot at the Tuesday metrics meeting. For each risk: has the early-warning indicator triggered, has the mitigation been executed, has severity or likelihood changed. New risks are added as they surface — the register is expected to grow during the pilot, and a register that does not grow is a register nobody is reading.
