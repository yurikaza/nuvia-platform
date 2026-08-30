# Operations — Phase 1

> Phase 1 operations are deliberately **semi-manual**. A human operations coordinator sits in the middle of every loop. This is correct: manual operations reveal what actually needs automating.

## 1. Core Workflow

```text
DIETITIAN CREATES PLAN
        ↓
SYSTEM GENERATES WEEKLY BASKET
        ↓
DIETITIAN REVIEWS
        ↓
CUSTOMER REVIEWS + APPROVES
        ↓
SUPPLIERS PREPARE
        ↓
COURIER COLLECTS FROM SUPPLIERS
        ↓
COURIER DELIVERS TO CUSTOMER
        ↓
CUSTOMER SEES PACKAGE
        ↓
CUSTOMER PAYS VIA COURIER SOFTPOS
        ↓
PAYMENT CONFIRMED
        ↓
SETTLEMENT PROCESS STARTS
        ↓
CUSTOMER CONTINUES
```

The customer **approves before preparation but pays at delivery**. This is the Phase 1 payment model.

## 2. Weekly Operating Calendar

| Day | Time | Who | Action |
|---|---|---|---|
| Thursday | 09:00 | System | Generate next week's baskets |
| Thursday | 10:00 | Dietitians | Review and confirm |
| Thursday | 12:00 | System | Send baskets to customers |
| Thu–Fri | — | Customers | Review, approve, swap or skip |
| Friday | 18:00 | — | Approval cutoff |
| Friday | 19:00 | System | Aggregate supplier pick lists |
| Friday | 20:00 | Ops | Send lists and confirm supplier acceptance |
| Saturday | 09:00 | Ops | Build routes and assign couriers |
| Saturday | 10:00 | Couriers | Routes visible before shift |
| Sunday | 08:00 | Suppliers | Orders ready |
| Sunday | 09:00 | Couriers | Collect and verify |
| Sunday | 10:00–16:00 | Couriers | Deliver + SoftPOS payment |
| Sunday | After route | Ops | Reconcile deliveries, payments and exceptions |
| Monday | — | Ops | Complaints, refunds and settlement reconciliation |
| Tuesday | — | Ops | Metrics and partner check-ins |

Phase 1 uses one consolidated delivery day to protect route density. Add another day only after route capacity justifies it.

## 3. Supplier Preparation

Approved customer baskets are aggregated by supplier. Ops sends a consolidated pick list and requires explicit acceptance.

The supplier is being asked to release goods to the courier **before the customer payment**. This must therefore be a negotiated commercial term, not an assumed right.

The supplier agreement must state:

- approved order value;
- pickup time;
- product/portion specifications;
- what happens if an item is short;
- what happens if the customer refuses payment;
- target settlement window after successful SoftPOS payment;
- maximum outstanding exposure Nuvia may create.

### Supplier trust model

Start with small limits. As successful transactions accumulate, increase the supplier's permitted exposure.

```text
First orders → small exposure cap
        ↓
Successful deliveries + settlements
        ↓
Supplier confidence
        ↓
Higher exposure / larger weekly volume
```

The target settlement window is approximately **30 minutes**, subject to PSP and banking capabilities. Nuvia must not promise a bank-transfer SLA until the payment provider confirms it contractually.

## 4. Route Planning

Saturday: ops clusters customers geographically and creates the route.

The courier knows before starting:

- all stops;
- addresses/map pins;
- delivery windows;
- route order;
- expected pay;
- supplier pickup points.

This predictability is the courier value proposition. Nuvia is not competing on instant delivery.

## 5. Delivery + Payment

At each stop:

1. Courier arrives.
2. Customer receives the package.
3. Customer can verify that the package corresponds to the approved basket.
4. Courier initiates SoftPOS payment for the exact order amount.
5. Payment success is confirmed.
6. Courier marks the delivery complete.
7. Nuvia records the payment reference and starts the settlement process.

The customer should see in the app:

> **Payment due at delivery**

before the courier arrives, then:

> **Payment successful — order completed**

after the transaction.

### No normal cash collection

Cash should not be the default. If an exceptional cash flow is supported during the pilot, it must be separately reconciled and must not become the core process.

## 6. Payment / Settlement

The target flow is:

```text
Customer SoftPOS payment
        ↓
Payment confirmed
        ↓
Order marked paid
        ↓
Settlement ledger created
        ├── Supplier A
        ├── Supplier B (if applicable)
        ├── Courier
        ├── Dietitian (~5%)
        └── Nuvia
```

The payment provider should handle the regulated payment acceptance and any supported marketplace/split settlement mechanism. Nuvia should not create its own wallet or informal escrow system.

See [`PAYMENT_AND_SETTLEMENT.md`](./PAYMENT_AND_SETTLEMENT.md) for provider validation and legal questions.

## 7. Customer Support

Customer-facing support lives primarily inside the Nuvia app, with WhatsApp/phone as Phase 1 operational fallbacks.

Important cases:

| Case | Action |
|---|---|
| Missing item | Record item-level issue; resolve/refund according to policy |
| Quality problem | Escalate immediately; log supplier/product |
| Wrong quantity | Record discrepancy and adjust |
| Payment failure | Retry under controlled flow; contact ops before leaving unpaid delivery |
| Customer refuses package | Record refusal; do not mark successful delivery/payment |
| Wants plan change | Route to dietitian; Nuvia does not make clinical changes |
| Wants pause/cancel | Self-service in app; capture reason |

## 8. Quality Control

Checks occur at supplier selection, pickup, delivery and post-delivery feedback.

The courier's pickup verification should catch missing/incorrect items before the route starts whenever possible.

Cold-chain handling, food safety and complaint escalation must follow applicable Turkish requirements and supplier agreements.

## 9. Roles

| Role | Phase 1 responsibility |
|---|---|
| Operations coordinator | Weekly execution, suppliers, routes, exceptions, reconciliation |
| Founder / partner manager | Dietitians, gyms, suppliers and key customer feedback |
| Product / engineering | Customer app, dietitian dashboard, ops and courier interface |
| Couriers | Planned routes, pickup verification, delivery and SoftPOS payment |
| Suppliers | Preparation, portioning, quality and agreed pre-payment release |

## 10. Critical Operational Rule

**Never surprise a participant.**

The customer knows the basket and payment timing. The supplier knows the order value and settlement promise. The courier knows the route and expected pay. The dietitian knows which clients are active and what was ordered.

Predictability is the operating system of Nuvia Phase 1.
