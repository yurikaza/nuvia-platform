# Gold Cluster Strategy — Phase 1

> **Status: strategic planning / validation hypothesis**
>
> Phase 1 should not attempt to cover Atakum uniformly. We should identify and concentrate operations in small, geographically dense micro-markets where demand, protein supply, complementary grocery supply, and courier routes reinforce each other.

---

## 1. Definition

A **Gold Cluster** is a compact geographic area containing enough of the following to support an economically viable Phase 1 launch:

1. **Demand nodes** — one or more independent dietitians / nutrition practices.
2. **Protein supply nodes** — preferably multiple chicken suppliers / poultry shops / butchers.
3. **Basket-completion nodes** — one or more competitive medium-sized local markets.
4. **Customer density** — meaningful residential density around the cluster.
5. **Courier feasibility** — short practical pickup and delivery routes.

The original "Gold Triangle" is therefore the core pattern:

```text
                 DIETITIAN(S)
                      │
                      │ demand
                      ↓
             ┌─────────────────┐
             │     CLUSTER     │
             └─────────────────┘
                ↙           ↘
       PROTEIN SUPPLY    MEDIUM MARKET
       chicken/butcher   basket completion
                ↘           ↙
                 COURIER NETWORK
                      ↓
                  CUSTOMERS
```

The **triangle is not the final unit of analysis**. Residential density, supplier redundancy, basket coverage and courier route efficiency determine whether the triangle is commercially useful.

---

## 2. Why Clusters Matter

The Phase 1 model deliberately avoids owning a warehouse or cold-chain network. The supplier network becomes the distributed fulfillment layer.

A strong cluster lets Nuvia approximate a local fulfillment centre without physically owning one:

```text
                 NUVIA
                   │
          demand aggregation
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   Dietitian    Chicken     Market
   demand       supplier    supplier
       │           │           │
       └───────────┼───────────┘
                   ↓
             Planned routes
                   ↓
               Customers
```

The objective is not minimum delivery count at all costs. The objective is **low fulfillment cost per completed order while preserving customer convenience**.

---

## 3. Gold Cluster Components

### 3.1 Demand density

Prioritise locations with:

- multiple independent dietitians;
- multiple dietitians in the same building or immediate area;
- clinics serving a meaningful number of clients;
- dense residential buildings around the practices;
- evidence of nutrition-plan / structured-diet demand.

Do not infer exact customer counts from public listings. Treat customer volume as a validation question.

### 3.2 Protein supply density

Protein is the Phase 1 wedge because chicken is expected to be a high-frequency component of nutrition plans.

Prefer clusters with **2 primary protein suppliers plus 1 backup/overflow candidate** where practical.

Supplier selection is based on:

- product quality;
- operational reliability;
- cold-chain capability;
- preparation and portioning capability;
- available capacity headroom;
- willingness to provide predictable pricing;
- willingness to work with Nuvia's planned-order process.

A financially pressured but operationally sound business can be attractive because Nuvia can fill unused capacity. Financial distress alone is never a supplier-selection criterion.

### 3.3 Basket-completion density

Medium-sized local markets provide products that a chicken supplier does not normally carry:

- oats;
- rice;
- legumes;
- dairy;
- eggs;
- vegetables and fruit;
- other ordinary grocery products.

The market is a **basket-completion partner**, not merely another supplier.

### 3.4 Residential density

A cluster with many businesses but few nearby households is weak.

Prioritise areas where potential customers are concentrated in apartment buildings or other dense residential areas.

The relevant question is:

> **How many potential customer addresses can one short courier route serve?**

### 3.5 Courier geometry

Use practical route distance rather than only straight-line distance when available.

Evaluate:

- supplier-to-supplier distance;
- supplier-to-customer distance;
- customer-to-customer route density;
- road / walking access;
- major-road barriers;
- pickup loading practicality;
- expected stops per route.

Straight-line distance is acceptable for initial screening; route distance should be used for high-ranking candidates.

---

## 4. Supplier Redundancy

Never make one chicken supplier the single point of failure for a cluster when alternatives exist.

Target structure:

```text
             Protein demand
                    │
          ┌─────────┼─────────┐
          ↓         ↓         ↓
       Supplier A Supplier B Supplier C
       primary    primary    backup
```

The exact allocation can change with capacity and price.

For example:

- A handles the majority of weekly volume;
- B handles the remainder;
- C absorbs overflow or disruption.

Multiple suppliers also create a real pricing benchmark and reduce dependence on a single commercial relationship.

---

## 5. Courier Model Inside a Cluster

A customer may want the entire weekly basket on one day even when the basket comes from multiple suppliers.

This is acceptable.

Example:

```text
Customer weekly basket
        │
        ├── Protein → Courier A → Chicken supplier
        │
        └── Grocery → Courier B → Medium market
                         │
                         └── same delivery window
```

Nuvia may use multiple couriers for one customer/order when necessary. The extra courier cost is a variable fulfillment cost; it should not be treated as a structural blocker if the order contribution remains healthy.

Where route density allows, multiple customer orders should be grouped at the supplier pickup stage and then distributed through planned routes.

The preferred operational metric is:

> **Fulfillment cost per completed order**

not simply:

> deliveries per customer.

A split delivery on the same day can be preferable to forcing a customer into two separate shopping days.

---

## 6. Gold Cluster Scoring

The initial score should be transparent and configurable.

### Demand

- dietitian count;
- dietitian density;
- evidence of active practice;
- surrounding residential density.

### Supply

- chicken supplier count;
- butcher count;
- supplier redundancy;
- supplier proximity;
- estimated/validated capacity headroom.

### Basket coverage

- medium-market count;
- proximity to protein suppliers;
- breadth of ordinary grocery categories;
- price competitiveness versus major chains where evidence is available.

### Logistics

- practical route distance;
- customer address density;
- expected stops per route;
- pickup accessibility;
- ability to serve a cluster with multiple couriers.

### Partnership potential

- supplier willingness to cooperate;
- market willingness to provide platform pricing / reserved inventory;
- dietitian willingness to refer clients;
- quality of owner/operator relationship.

Do not use a black-box model in Phase 1. Every score must be explainable.

---

## 7. Suggested Initial Score

This is a starting hypothesis, not a permanent formula.

| Dimension | Weight |
|---|---:|
| Demand density | 25 |
| Protein supply + redundancy | 25 |
| Grocery / basket coverage | 15 |
| Residential/customer density | 15 |
| Courier efficiency | 10 |
| Partnership potential | 10 |
| **Total** | **100** |

Within each dimension, use evidence-backed sub-scores.

Do not award capacity points when capacity is unknown. Record:

- `verified`
- `estimated`
- `unknown`

rather than inventing numbers.

---

## 8. Cluster Validation Workflow

Discovery is not the same as validation.

```text
MAP DATA
   ↓
NORMALIZE BUSINESSES
   ↓
DETECT CLUSTERS
   ↓
RANK CLUSTERS
   ↓
HUMAN MAP REVIEW
   ↓
FIELD CHECK
   ↓
DIETITIAN INTERVIEW
   ↓
SUPPLIER INTERVIEW
   ↓
MARKET INTERVIEW
   ↓
COURIER ROUTE TEST
   ↓
PILOT CLUSTER
```

For every top candidate, record:

- businesses found;
- actual existence confirmed;
- category confirmed;
- route distances checked;
- supplier capacity status;
- supplier commercial interest;
- market commercial interest;
- dietitian interest;
- estimated customer density;
- operational blockers;
- final decision: `pilot / watch / reject`.

---

## 9. Phase 1 Geographic Strategy

Do not launch across all of Atakum simultaneously.

Preferred approach:

1. Find the strongest Gold Cluster.
2. Validate it manually.
3. Establish enough supplier redundancy.
4. Recruit dietitian demand inside/near the cluster.
5. Run the first operational pilot.
6. Measure fulfillment cost, basket economics and repeat ordering.
7. Expand to the next adjacent high-scoring cluster.

The first objective is **density, not geographic coverage**.

---

## 10. Data Sources and Legitimacy

Use legitimate data sources and respect applicable terms and privacy requirements.

Potential sources:

- official Places / business APIs where permitted;
- OpenStreetMap / Overpass;
- public municipal/open datasets;
- publicly available business information.

Do not scrape Google Maps or another service in a way that violates its terms.

Public business listings are discovery evidence, not ground truth.

Do not collect unnecessary personal information about individual dietitians or customers.

---

## 11. Core Research Questions

Every Gold Cluster analysis should eventually answer:

1. How much demand can this area plausibly generate?
2. How many independent protein suppliers can serve it?
3. Can at least two protein suppliers operate reliably?
4. Can a nearby market complete most non-protein baskets?
5. How dense are customer addresses?
6. How many orders can one planned route serve?
7. What happens when one supplier is unavailable?
8. Can the cluster support one-day multi-supplier delivery?
9. What is the likely fulfillment cost per order?
10. Which commercial relationships must be negotiated before launch?

---

## 12. Non-Goals

Phase 1 Gold Cluster discovery does **not** attempt to:

- build a nationwide marketplace;
- include gyms as a Phase 1 acquisition channel;
- operate a warehouse;
- operate a cold-chain facility;
- predict exact supplier capacity from map data;
- replace human supplier validation;
- build ML-based geographic prediction.

The output is a ranked set of **validated micro-markets for launch**.
