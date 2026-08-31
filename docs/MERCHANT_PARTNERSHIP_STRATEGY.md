# Merchant Partnership Strategy — Phase 1

> Medium-sized local markets are **basket-completion partners** inside the Gold Cluster model, not a fallback catalogue.

## 1. Objective

Use a small number of reliable local markets to complete the non-protein portion of weekly nutrition baskets without owning a warehouse.

Ideal merchants are:
- close to protein suppliers and dense customer addresses;
- larger/more organised than a small neighbourhood bakkal;
- competitive with major chains on at least some everyday products;
- able to batch-prepare orders before a fixed pickup time;
- willing to negotiate based on predictable recurring volume;
- owner-operated or managed by someone able to make commercial decisions quickly.

The goal is **competitive cluster-level economics**, not beating BİM/A101/ŞOK/Migros on every SKU.

## 2. Merchant Value Proposition

> **"We bring you recurring, planned basket volume without requiring you to acquire those customers."**

Nuvia provides:
- forecastable weekly demand;
- consolidated orders;
- a digital sales channel;
- courier pickup;
- potential recurring volume growth.

The merchant provides:
- existing inventory and storage;
- product availability;
- order preparation;
- pickup-ready handoff.

## 3. Commercial Models to Test

### A. Platform-specific price

Merchant gives Nuvia an agreed price on selected high-frequency products.

### B. Volume-tier pricing

Commercial terms improve as recurring weekly volume grows. Exact discounts are negotiation hypotheses, not commitments.

### C. Merchant price + transparent platform margin/fee

Useful when the merchant strongly protects retail pricing but values incremental volume.

### D. Reserved inventory

For selected high-frequency products, the merchant reserves an agreed quantity for the upcoming fulfillment window. This creates **virtual inventory** without Nuvia owning a warehouse.

Do not reserve stock unless reliability and commercial terms justify it.

## 4. Product Strategy

Do not expose the whole store catalogue in Phase 1. Start from actual dietitian baskets and build a curated high-frequency list.

Potential categories:
- oats;
- rice;
- pasta;
- legumes;
- dairy;
- eggs;
- vegetables and fruit;
- sauces and pantry items;
- other repeatedly requested groceries.

The catalogue should follow **observed basket demand**, not store breadth.

## 5. Merchant Selection

Score candidates on:

| Dimension | Importance |
|---|---:|
| Distance to protein supplier | Very high |
| Distance to customer cluster | Very high |
| Product coverage | High |
| Price competitiveness | High |
| Stock reliability | High |
| Batch preparation capability | High |
| Owner/manager accessibility | High |
| Willingness to negotiate | High |
| Capacity headroom | Medium |

A slightly more expensive merchant can be superior if it is much closer, more reliable and easier to operate with.

## 6. Gold Cluster Integration

The strongest merchant is the one that improves **cluster-level economics**, not necessarily the one with the lowest isolated shelf price.

```text
2–3 Dietitians
      ↓
Customer demand
      ↓
2+ Protein suppliers
      ↓
Medium market
      ↓
Dense customer addresses
      ↓
Planned courier routes
```

The market becomes part of a distributed fulfillment cell: Nuvia has no warehouse, but the cluster has local physical inventory that can be accessed on demand.

## 7. Order Preparation

Nuvia sends a consolidated pick list before the agreed cutoff.

Example:

```text
Nuvia — Thursday pickup

Oats        18 units
Rice        14 units
Yoghurt     32 units
Eggs        21 packs
Bananas     15 kg
Legumes      9 kg
```

The merchant batch-prepares the order and marks it pickup-ready. The courier verifies order count, obvious quantity discrepancies and packaging condition before leaving.

Food-safety and cold-chain requirements remain subject to applicable Turkish requirements and the merchant agreement.

## 8. Stock-Out and Substitution Policy

For every product define:
1. exact product;
2. acceptable substitute, if any;
3. whether substitution requires customer/dietitian approval;
4. refund/credit treatment;
5. merchant responsibility for unavailable stock.

A merchant must not silently replace a dietitian-specified item with an arbitrary alternative. Clinically relevant substitutions remain a dietitian decision where applicable.

## 9. Negotiation Principles

Negotiate from **forecastable volume**, not desperation.

The core commercial conversation:

> "We aggregate orders before fulfillment. You know the volume before you prepare it, and our couriers collect it. In return for recurring volume and low customer-acquisition burden, what platform price can you offer us on the products we repeatedly order?"

Avoid blanket discounts. First identify 10–30 high-frequency products and compare:
- current merchant price;
- possible platform price;
- expected weekly quantity;
- stock reliability;
- contribution to the typical basket.

## 10. Relationship Strategy

Local merchant relationships are long-term operating assets.

```text
Recurring demand
      ↓
Merchant revenue
      ↓
Trust
      ↓
Better commercial terms
      ↓
Better customer economics
      ↓
More demand
```

Reliable payment, respectful communication and transparent expectations matter alongside price. Do not request exclusivity before Nuvia has earned it.

## 11. Payment / Settlement

Before accepting an order, the merchant should know:
- order value;
- pickup date/time;
- expected settlement timing;
- shortage/refusal treatment;
- maximum outstanding exposure.

Do not promise a settlement SLA until the payment provider and banking flow support it. See [`PAYMENT_AND_SETTLEMENT.md`](./PAYMENT_AND_SETTLEMENT.md).

## 12. Metrics

### Commercial
- platform price vs merchant shelf price;
- negotiated spread/discount;
- weekly order value;
- basket coverage.

### Operational
- fill rate;
- stock-out rate;
- pickup-ready-on-time rate;
- quantity discrepancy rate;
- substitution rate;
- merchant-caused complaint rate.

### Relationship
- response time;
- payment reliability;
- willingness to increase volume;
- owner/manager satisfaction;
- continuation after pilot.

## 13. Phase 1 Target

For the first validated Gold Cluster:
- 1 primary medium market;
- 1 backup market where practical;
- curated high-frequency product list;
- fixed pickup window;
- agreed platform pricing on selected products;
- explicit stock-out/substitution rules;
- measured fill rate and fulfillment cost.

Reliability and cluster density beat catalogue breadth.

## 14. Non-Goals

Phase 1 does not attempt to:
- become a general grocery marketplace;
- list every SKU in every store;
- guarantee prices below every national chain;
- hold merchant inventory ourselves;
- request premature exclusivity;
- replace dietitian judgment on clinically relevant substitutions.

> **Use a small number of reliable local merchants to complete real weekly nutrition baskets inside dense Gold Clusters, without owning a warehouse.**
