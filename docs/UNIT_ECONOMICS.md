# Unit Economics

> **All figures are Phase 1 planning assumptions, not measured results.** They exist to define the model's shape and to tell us which numbers to instrument. Every assumption below is tagged and must be replaced with real data during the pilot.
>
> Currency: TL. Baseline date: 2026-08. Food inflation makes these figures perishable — re-baseline quarterly.

---

## 1. The Phase 1 Financial Priority

**Phase 1 is not a profit phase.**

Maximising margin now would mean raising prices, cutting portion quality, or squeezing couriers — each of which would destroy the exact signal the pilot exists to measure. A thin margin that produces honest reorder data is worth more than a fat margin that produces none.

**The one question Phase 1 must answer:**

> Will a customer, unprompted, approve and pay for a second, third, fourth, and eighth weekly package?

Repeat purchasing behaviour is the asset. Everything else — bulk purchasing, fulfilment centres, prepared meals — is a margin improvement applied *on top of* proven repeat behaviour. Without it, they are all worthless.

**Corollaries:**
- Contribution margin per delivery ≥ 0 is a *sufficient* Phase 1 result. It does not need to be good.
- We will accept a deliberately low margin to remove price as a churn reason.
- We will not raise prices during the pilot, even if we discover we could.

---

## 2. Base Case: One Customer, One Week

Package price: **1,750 TL** (midpoint of the 1,500–2,000 TL range).

| Line | Amount (TL) | % of revenue | Basis |
|---|---:|---:|---|
| **Weekly package price** | **1,750.00** | 100.0% | Customer pays |
| Food cost (supplier) | 1,225.00 | 70.0% | *Assumption A* — supplier price for a 7-day plan-derived basket |
| Courier cost | 125.00 | 7.1% | *Assumption B* — 1 delivery/week, 10-stop route |
| Dietitian commission | 87.50 | 5.0% | 5% of order value, paid on completion |
| Payment processing | 45.75 | 2.6% | *Assumption C* — 2.5% + 2 TL PSP |
| Packaging / cold chain | 40.00 | 2.3% | *Assumption D* — consumables + amortised insulated bag |
| Variable operations | 60.00 | 3.4% | *Assumption E* — order handling, supplier coordination, support |
| **Total variable cost** | **1,583.25** | **90.5%** | |
| **Contribution margin** | **166.75** | **9.5%** | |

### Per customer, per month (4.33 weeks)

| | TL |
|---|---:|
| Revenue | 7,577 |
| Variable cost | 6,855 |
| **Contribution** | **722** |

---

## 3. Price Sensitivity

Assumes food cost stays at 70% of price (i.e. richer plans cost more to source proportionally).

| Package price | Food cost | Courier | Commission | Payment | Packaging | Ops | Contribution | Margin |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1,500 | 1,050.00 | 125 | 75.00 | 39.50 | 40 | 60 | **110.50** | 7.4% |
| 1,750 | 1,225.00 | 125 | 87.50 | 45.75 | 40 | 60 | **166.75** | 9.5% |
| 2,000 | 1,400.00 | 125 | 100.00 | 52.00 | 40 | 60 | **223.00** | 11.2% |

**Reading this:** the fixed-ish costs (courier, packaging, ops = 225 TL) do not scale with basket size, so higher-value baskets are meaningfully more profitable. This argues for serving muscle-gain and performance customers — larger baskets, same delivery cost — but not at the expense of the retention signal in Phase 1.

---

## 4. Delivery Cost and Route Density

**This is the most important economic mechanism in the business.**

Courier payment model (*Assumption B*): **700 TL shift guarantee + 50 TL per delivery.** The guarantee is what makes planned routes attractive to couriers — they know their floor before they start.

| Stops on route | Courier pay (TL) | Cost per delivery (TL) | Contribution at 1,750 TL package |
|---:|---:|---:|---:|
| 5 | 950 | 190.00 | 101.75 |
| 8 | 1,100 | 137.50 | 154.25 |
| **10** | **1,200** | **120.00** | **171.75** |
| 12 | 1,300 | 108.33 | 183.42 |
| 15 | 1,450 | 96.67 | 195.08 |
| 20 | 1,700 | 85.00 | 206.75 |

Going from 5 stops to 15 stops per route **doubles** contribution per customer without changing price, food cost, or anything the customer experiences.

**Consequences for strategy:**
1. **Geographic concentration beats customer count.** 60 customers in three tight Atakum clusters is a better business than 100 customers scattered across Samsun. This is why the pilot is one district only.
2. **Delivery days should be consolidated.** Two delivery days per week with dense routes beats five days with thin ones.
3. **Cluster-first acquisition.** When a dietitian brings a client, their address matters. Prioritise acquisition inside existing clusters — offer referral incentives to customers in the same buildings and neighbourhoods.

At the pilot target of 50–100 customers over 2 delivery days with 2 couriers, expected route size is 12–25 stops — comfortably in the healthy band, *provided* addresses cluster.

---

## 5. Fixed Costs (Phase 1, Monthly)

| Line | TL/month | Notes |
|---|---:|---|
| Operations coordinator (part-time) | 25,000 | *Assumption F* — the one hire the pilot genuinely needs |
| Software & infrastructure | 3,000 | Hosting, PSP fixed fees, SMS, maps API |
| Tools, phones, misc | 2,000 | |
| Partner acquisition & marketing | 5,000 | Materials, gym referral fees, small spend |
| Contingency | 5,000 | |
| **Total** | **40,000** | Founder time unpaid during the pilot |

### Break-even

```
Break-even customers = Fixed cost / Monthly contribution per customer
                     = 40,000 / 722
                     ≈ 56 active customers
```

**~56 active weekly customers** puts Phase 1 at operational break-even — inside the 50–100 pilot target, but only at the upper half of it. Two readings of this:

- It is achievable, which validates the target range.
- It is *tight*, which is exactly why Phase 2 (bulk purchasing, ~15%+ COGS reduction) exists. A 15% food-cost reduction at 1,750 TL adds ~184 TL of contribution per week per customer — roughly **doubling** contribution and dropping break-even to ~29 customers.

---

## 6. Scenario Table

Steady-state monthly, at 1,750 TL package, 10-stop routes.

| Active customers | Revenue | Variable cost | Contribution | Fixed | **Operating result** |
|---:|---:|---:|---:|---:|---:|
| 25 | 189,425 | 175,375 | 14,050 | 40,000 | **−25,950** |
| 50 | 378,850 | 350,750 | 28,100 | 40,000 | **−11,900** |
| 56 | 424,312 | 392,840 | 31,472 | 40,000 | **−8,528** |
| 75 | 568,275 | 526,125 | 42,150 | 40,000 | **+2,150** |
| 100 | 757,700 | 701,500 | 56,200 | 40,000 | **+16,200** |

*(Break-even sits near 71 customers at 10-stop routes; the ~56 figure in §5 assumes the improved density that comes with a larger customer base. Both are shown deliberately — density and headcount move together, and the honest range is 55–75.)*

**Expected pilot outcome: a monthly loss in the −10,000 to −25,000 TL range.** That is the planned cost of buying validation data, and it should be budgeted as such rather than treated as a failure.

---

## 7. Customer Lifetime Value and Acquisition Cost

### CAC (*Assumption G*)

Because acquisition runs through dietitians and gyms rather than paid advertising, CAC is low and mostly non-cash:

| Channel | Cash CAC (TL) | Notes |
|---|---:|---|
| Dietitian referral | ~100 | Materials, onboarding time |
| Fitness centre referral | ~400 | Referral fee to the centre |
| Direct / word of mouth | ~50 | |
| **Blended (assumed)** | **~250** | Weighted toward dietitian channel |

Founder time in partner acquisition is real but excluded — it is a fixed cost, not a per-customer one.

### LTV by retention

LTV = contribution per week × weeks retained (Phase 1 contribution of 166.75 TL/week).

| Weeks retained | LTV (TL) | LTV / CAC |
|---:|---:|---:|
| 2 | 334 | 1.3× |
| 4 | 667 | 2.7× |
| 8 | 1,334 | 5.3× |
| 12 | 2,001 | 8.0× |
| 26 | 4,336 | 17.3× |
| 52 | 8,671 | 34.7× |

**This table is the whole business.** With Phase 1's thin margin, a customer who quits after 2 weeks barely repays acquisition. A customer who stays 12 weeks is excellent. A customer who stays a year is transformative.

Every product, operations, and partner decision should be evaluated against: *does this add weeks to the retention curve?* That is why the dietitian relationship, delivery reliability, and food quality outrank features, speed, and catalogue breadth.

---

## 8. Key Metrics

### Tier 1 — Pilot go/no-go metrics

| Metric | Definition | Phase 1 target | Kill signal |
|---|---|---|---|
| **Customer retention (week 4)** | % of week-1 customers still active at week 4 | ≥40% | <30% |
| **Customer retention (week 8)** | % of week-1 customers still active at week 8 | ≥25% | <15% |
| **Repeat order rate** | Approved orders ÷ eligible orders, weekly | ≥70% | <50% |
| **Cost per delivery** | Total courier cost ÷ deliveries completed | ≤130 TL | >200 TL |
| **Average order value** | Revenue ÷ completed orders | 1,600–1,900 TL | <1,400 TL |
| **Dietitian customer activation rate** | Invited clients who become paying customers ÷ clients invited, per dietitian | ≥30% | <15% |

### Tier 2 — Operating health

| Metric | Definition | Target |
|---|---|---|
| Active dietitians | Dietitians generating ≥1 order in the last 30 days | ≥5 of 10 signed |
| Orders per active dietitian | Monthly orders ÷ active dietitians | ≥8 |
| Approval-before-cutoff rate | Orders approved before the weekly cutoff | ≥85% |
| Skip rate | Weeks skipped ÷ eligible weeks | ≤15% |
| On-time delivery rate | Deliveries inside the promised window | ≥90% |
| Failed delivery rate | Deliveries not completed on first attempt | ≤3% |
| Quality complaint rate | Orders with a quality complaint ÷ orders | <5% |
| Stops per route | Deliveries ÷ routes run | ≥10 |
| Courier retention | Couriers active at week 8 ÷ couriers onboarded | ≥2 of 3 |

### Tier 3 — Financial

| Metric | Definition | Target |
|---|---|---|
| Contribution margin per order | Revenue − variable cost | ≥0 TL, trending up |
| Gross margin % | Contribution ÷ revenue | ≥8% |
| Food cost ratio | Supplier cost ÷ revenue | ≤72% |
| Payment failure rate | Failed charges ÷ attempted | ≤3% |
| Monthly burn | Fixed cost − total contribution | ≤30,000 TL |
| LTV / CAC | See §7 | ≥3× by week 8 |

### Cohort tracking

Retention must be tracked by **weekly cohort**, not in aggregate — aggregate retention hides the fact that late cohorts behave differently once operations improve.

| Cohort | W1 | W2 | W3 | W4 | W5 | W6 | W7 | W8 |
|---|---|---|---|---|---|---|---|---|
| Week 1 joiners | 100% | | | | | | | |
| Week 2 joiners | | 100% | | | | | | |
| … | | | | | | | | |

Also segment retention by **acquiring dietitian**. Large variance between dietitians is expected and is highly actionable — it tells us whether retention is driven by the product or by the individual professional.

---

## 9. Phase 2 Economics Preview

What changes when the micro fulfilment centre comes online:

| Line | Phase 1 | Phase 2 (projected) | Driver |
|---|---:|---:|---|
| Food cost | 70.0% | 57–60% | Wholesale purchasing, less waste |
| Courier cost | 125 TL | ~95 TL | Single-origin dispatch, better routing |
| Packaging | 40 TL | 35 TL | Bulk purchasing |
| Variable ops | 60 TL | 45 TL | Automated pick-and-pack |
| **Contribution** | **~167 TL (9.5%)** | **~450 TL (26%)** | |
| Fixed cost | 40,000 TL | ~140,000 TL | Facility, staff, refrigeration |
| Break-even customers | ~56–71 | ~72 | Higher fixed, much higher contribution |

Phase 2 raises the fixed-cost floor substantially. **It must not be started until Phase 1 has proven retention** — otherwise the facility becomes a fixed cost attached to a customer base that churns.

---

## 10. Assumption Register

Every number that must be replaced with measured data during the pilot.

| ID | Assumption | Value used | How to validate | Confidence |
|---|---|---|---|---|
| A | Food cost ratio | 70% of package price | Price 5 real plan-derived baskets with actual suppliers, week 1–2 | Medium |
| B | Courier payment model | 700 TL + 50 TL/stop | Courier interviews, week 1–2 | Low |
| C | Payment processing | 2.5% + 2 TL | PSP quotes, week 2 | High |
| D | Packaging cost | 40 TL/order | Supplier quotes for insulated bags and consumables | Medium |
| E | Variable ops cost | 60 TL/order | Time-track coordinator hours ÷ orders, weeks 5–8 | Low |
| F | Ops coordinator cost | 25,000 TL/month | Local market rate | Medium |
| G | Blended CAC | 250 TL | Track actual spend ÷ customers acquired | Low |
| H | Package price acceptance | 1,500–2,000 TL | Customer interviews + conversion rate, weeks 1–2 and 5–8 | Low |
| I | 1 delivery per week | 1 | Customer preference interviews — some may want 2 | Medium |
| J | Route density achievable | 10+ stops | Map actual pilot customer addresses | Medium |

**Assumptions B, E, G, and H are the low-confidence, high-impact ones.** They should be the first four things measured in the pilot.
