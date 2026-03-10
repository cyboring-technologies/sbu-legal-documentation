---
id: "STRIPE_PAYMENT_FLOW"
title: "Stripe Payment Flow Architecture"
type: "Execution Principles and Token Models"
version: "v1.0"
last_updated: "2026-03-09"
status: "Approved"
---

# Stripe Payment Flow Architecture

**Context:** *This document defines the operational Stripe payment flow, the Rubicon event, and execution token issuance rules for crossing the payment boundary.*

---

# 1. Purpose

This document defines the **operational Stripe payment flow** used by the SBU‑Legal system.

It describes:

- PaymentIntent lifecycle
- The Rubicon event (authority acquisition)
- Execution token issuance
- Payment capture and cancellation logic
- Failure handling

This document describes **payment mechanics only**.  
Business meaning and execution semantics are defined in:

- `BASE_EXECUTION_CONTRACT.md`
- `README_GATEWAY_V2.md`
- `README_ENGINE_V2.md`

---

# 2. Conceptual Role of Payment

In the SBU‑Legal system:

Payment is **not access**.

Payment is **authority**.

Crossing the payment boundary grants the Engine the authority to perform a **single irreversible execution**.

This event is called the **Rubicon**.

---

# 3. Stripe Integration Model

Stripe is used exclusively for:

- Payment authorization
- Payment capture
- Payment cancellation
- Dispute handling

Stripe never stores:

- documents
- prompts
- drafts
- user data

Stripe only processes the financial transaction.

---

# 4. Payment Architecture

Components involved in payment:

```
Client (Engine UI)
        |
        v
Gateway Worker
        |
        v
Stripe PaymentIntent API
        |
        v
Execution Token Issuance
        |
        v
Engine Post‑Authority Execution
```

---

# 5. PaymentIntent Creation

The payment lifecycle begins when the user confirms execution.

The Engine requests the Gateway to create a PaymentIntent.

Stripe configuration:

```
capture_method = manual
```

This creates an **authorization hold** rather than immediate capture.

Purpose:

- Allows the system to cancel payment if execution fails.
- Prevents charging the user if no artifact is generated.

Example parameters:

```
amount
currency
capture_method: manual
automatic_payment_methods: enabled
```

---

# 6. Rubicon Event

The **Rubicon** occurs when:

```
PaymentIntent confirmed
AND
Gateway validates payment authorization
```

At this moment:

1. Payment authority exists
2. Gateway issues an **Execution Token**
3. Engine transitions to **Post‑Authority State**

No UI change occurs.

Only execution authority changes.

---

# 7. Execution Token

Execution token properties:

```
single‑use
short TTL
non‑identifying
opaque
memory‑resident
```

The token authorizes exactly:

```
one irreversible execution
```

Token lifecycle:

```
issued → consumed → destroyed
```

The token is never stored in a database.

---

# 8. Post‑Authority Execution

Once authority is granted:

The Engine calls:

```
/execute_after_payment
```

Execution sequence:

```
1. Token validated
2. Document frozen
3. LLM generation begins
4. Draft produced
5. Validator executed
```

Only one generation attempt is permitted.

---

# 9. Payment Capture

If generation succeeds and the validator passes:

The Engine performs:

```
stripe.paymentIntents.capture()
```

This converts the authorization hold into a finalized charge.

Capture occurs **after artifact generation**.

---

# 10. Payment Cancellation

If execution fails at any stage after authorization:

The system calls:

```
stripe.paymentIntents.cancel()
```

Possible failure causes:

- LLM timeout
- validator failure
- worker crash
- token invalidation

Cancellation releases the authorization hold.

The customer is not charged.

---

# 11. Webhooks

Stripe webhooks may be used for:

- payment confirmation
- dispute notifications
- chargeback events

Typical webhook events:

```
payment_intent.succeeded
payment_intent.payment_failed
charge.dispute.created
```

Webhook validation must use:

```
STRIPE_WEBHOOK_SECRET
```

---

# 12. Dispute Handling

Stripe manages disputes through its own dashboard.

The system does not automatically handle disputes.

Operational monitoring must track:

- chargebacks
- refund requests
- dispute rates

The economic model assumes low dispute rates.

---

# 13. Failure Model

Possible failure classes:

| Failure | Result |
|---|---|
LLM failure | Payment canceled |
Validator failure | Payment canceled |
Worker crash | Payment canceled |
User abandonment before Rubicon | No charge |

The system guarantees:

```
No artifact → No charge
```

---

# 14. Operational Safeguards

The payment architecture ensures:

- no payment without authority
- no charge without artifact
- no retries after execution

These rules enforce the **one‑shot model**.

---

# 15. Deployment Checklist

Before production launch verify:

```
Stripe account activated
Live API keys configured
Webhook endpoint registered
Gateway Worker deployed
Engine Worker deployed
```

Test using Stripe test cards before switching to live keys.

---

# 16. Final Rule

Stripe exists for a single purpose:

```
authorize one irreversible execution
```

After execution:

```
payment captured
authority consumed
session incinerated
```

# 17. Orphan Authorization Protection

A rare edge case may occur if the Worker process terminates after payment authorization but before payment capture.

Possible causes include:

- Worker crash
- infrastructure failure
- unexpected runtime termination

In this situation:

- the PaymentIntent remains in an authorized state
- Stripe automatically releases the authorization hold after its expiration window

The system intentionally does not retry execution in this scenario.

Retrying execution would violate the One-Shot execution invariant.

Operational monitoring should periodically review authorized but uncaptured PaymentIntents through the Stripe dashboard.
