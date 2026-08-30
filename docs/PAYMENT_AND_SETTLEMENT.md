# Payment & Settlement — Phase 1

> **Confirmed Phase 1 model:** the customer pays at the door using the courier's SoftPOS. The supplier releases the prepared order to the courier before the customer payment, based on Nuvia's short settlement promise. Once delivery/payment is confirmed, Nuvia triggers the settlement flow to the relevant supplier(s), courier, dietitian, and Nuvia share.

This is a product/business-model decision, not yet a confirmed legal or PSP implementation. The exact acquiring, settlement, invoicing, and funds-flow structure must be validated with the chosen Turkish payment provider and a local advisor before launch.

## 1. The Intended Flow

```text
Weekly basket generated
        ↓
Customer reviews and approves package
        ↓
Order is accepted for the weekly route
        ↓
Suppliers prepare the order
        ↓
Courier collects goods from suppliers
        ↓
Supplier releases goods before customer payment
        ↓
Courier arrives at customer
        ↓
Customer inspects the delivered package
        ↓
Courier accepts card payment via SoftPOS
        ↓
Payment success confirmed
        ↓
Nuvia marks order as delivered + paid
        ↓
Settlement is initiated
   ├── supplier entitlement(s)
   ├── courier entitlement
   ├── dietitian commission
   └── Nuvia platform share
```

The important customer promise is:

> **You pay when your package is physically at your door.**

This removes the uncertainty of paying days before seeing the actual food while keeping the delivery itself cashless and fast.

## 2. Why SoftPOS Matters in This Model

SoftPOS is not a generic payment feature. It is the final step in the trust loop.

The courier's Android phone becomes the payment acceptance device. Current Turkish providers document SoftPOS/App2App capabilities for initiating and checking transactions, while SoftPOS solutions are designed for mobile field collection. citeturn698738search0turn698738search4

Phase 1 assumptions:

- customer pays only after seeing the package;
- courier does not handle cash in the normal flow;
- payment result is confirmed before the route stop is closed;
- payment receipt is visible to the customer;
- delivery and payment are linked to the same order ID.

## 3. The Supplier Trust Problem

The hardest non-technical part of this model is that a supplier may be asked to hand goods to a courier before receiving money.

Nuvia therefore needs a **supplier settlement promise**:

> "You release the prepared order to our courier. The customer pays at the door. Once the payment is confirmed, your settlement is triggered immediately / within the agreed short settlement window."

The target operational window is approximately **30 minutes**, but this is a business target, not a guaranteed banking settlement time. The exact timing must be confirmed with the payment provider and bank rails.

Supplier onboarding should explicitly cover:

- the handover moment;
- the maximum expected settlement delay;
- what happens if the customer refuses payment;
- what happens if the payment fails;
- who bears a failed-delivery / refused-payment loss;
- how refunds and quality adjustments are handled.

## 4. Supplier Release Policy

Suppliers should not be asked to take unlimited credit risk.

Phase 1 should start with one of these controlled policies:

### Policy A — Nuvia guarantee for trusted suppliers

Nuvia guarantees the supplier's approved basket value up to an agreed exposure limit. Best suited to the first partners once a reliable payment record exists.

### Policy B — Exposure cap

A supplier may release only up to a small outstanding balance until previous settlement has cleared.

### Policy C — Initial deposit / rolling reserve

For a cautious supplier, Nuvia can maintain a limited operational reserve while the model proves itself.

**Default approach:** start with Policy A for small pilot orders and a strict exposure cap. The goal is to make the supplier feel that the risk is tiny and measurable, not invisible.

## 5. Multi-Party Settlement Ledger

Every order must have explicit economic lines before the route begins:

```text
Order total
├── Supplier A payable
├── Supplier B payable (if applicable)
├── Courier payable
├── Dietitian commission (~5%)
└── Nuvia platform share
```

The system must store these as immutable order-level ledger entries. Do not recalculate historical payouts from the current percentage after the order is closed.

Required states:

```text
approved
→ ready_for_collection
→ collected
→ delivered_pending_payment
→ paid
→ settlement_pending
→ settled
```

Exception states:

```text
payment_failed
payment_refused
delivery_failed
partially_refunded
fully_refunded
manual_review
```

## 6. Customer App Payment UX

The customer app must make the payment state obvious.

Before delivery:

- order total;
- itemised basket;
- "Payment due at delivery";
- delivery window;
- no card charge yet.

During delivery:

- "Your courier is here";
- exact amount due;
- SoftPOS payment instruction;
- payment success state.

After payment:

- receipt/reference;
- supplier/payment breakdown where appropriate;
- order marked delivered;
- next week's subscription status.

## 7. Failure Handling

### Customer refuses the package

Courier records refusal reason. Order is not marked paid. Ops decides whether the customer is eligible for a retry, return, partial charge, or other resolution under the published policy.

### Card payment fails

The courier should retry only within a short controlled flow. If payment cannot be completed, the courier contacts ops before leaving the item as delivered.

### Supplier shortfall discovered at pickup

Do not wait until the customer's door. Resolve, substitute, or re-price before route departure.

### Customer disputes an item at the door

Courier should not negotiate nutritional changes. Record the discrepancy, deliver only when the order can still be accepted under the standing policy, and let ops resolve the commercial adjustment.

## 8. Legal / PSP Validation — Mandatory Before Production

Turkey's payment-services framework is governed by Law No. 6493 and related secondary regulations; payment services must be provided through authorised payment service providers. The current TCMB lists authorised payment and electronic-money institutions. citeturn951305search0turn951305search5

Before implementation, obtain written answers from at least two authorised providers on:

1. Can the courier's SoftPOS legally/contractually accept payment for this exact marketplace model?
2. Which entity is the merchant of record for the customer transaction?
3. Can the customer payment be routed or allocated to multiple beneficiaries?
4. Can supplier and courier entitlements be settled automatically after delivery/payment confirmation?
5. What is the actual settlement timing — not the marketing description?
6. Can payment acceptance and marketplace settlement be combined in one provider stack or do they require separate contracts?
7. Who issues the customer invoice/e-archive invoice for a multi-supplier basket?
8. What KYC/onboarding is required from suppliers, dietitians, and couriers?
9. How are refunds, chargebacks, and disputed deliveries handled?
10. What happens if a SoftPOS transaction succeeds but the network callback is delayed?

Nuvia should **not** hold customer money in an ordinary operating bank account and manually transmit it as if it were its own payment service. The licensed provider should implement the payment acceptance and settlement mechanism.

## 9. Phase 1 Product Decision

| Decision | Phase 1 |
|---|---|
| Customer pays before delivery | **No** |
| Customer pays at delivery | **Yes — default** |
| Courier SoftPOS | **Core** |
| Cash | Exception only; not the target flow |
| Customer sees package before payment | **Yes** |
| Supplier hands package to courier before customer payment | **Yes, under agreed exposure / settlement terms** |
| Target supplier settlement time | **~30 minutes, subject to provider/bank confirmation** |
| Dietitian commission | Settled from completed paid order |
| Nuvia margin | Remaining platform share after confirmed costs |

## 10. The Core Hypothesis

The payment innovation is not "SoftPOS" by itself.

The hypothesis is:

> **A customer is more comfortable paying at the door, after seeing the food, while suppliers are willing to release goods first because Nuvia reliably settles their payable shortly after the customer transaction.**

This is one of the first pilot hypotheses to test with both sides independently.
