---
id: "PRICING_EXECUTION_MODEL"
title: "Pricing Execution Model"
type: "Execution Principles & Token Models"
version: "v1.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Pricing Execution Model

**Context:** *Details the technical implementation of the pricing logic and the authority transition. It describes how the CostManifest is signed and how payment validates the issuance of an execution token.*

## 1. PURPOSE
This document defines the technical implementation of cost calculation, authority transition, and execution constraints within the SBU-Legal Sovereign Engine. It serves as the single source of truth for how the system charges for, authorizes, and limits execution in its current production state.

## 2. CANONICAL UNIT OF SALE
The system sells **one (1) irreversible execution** of the generative legal pipeline.
It does **not** sell:
*   Access to the software (SaaS).
*   Storage or hosting of documents.
*   Retries or edits.
*   Legal advice or outcomes.

The transaction is atomic: Payment exchanged for a single state transition from `PRE_AUTHORITY` to `POST_AUTHORITY`, resulting in either a final artifact or total incineration.

## 3. COST CALCULATION (PRE-RUBICON)
Costs are derived exclusively from the Engine's server-side analysis of the uploaded file. The client cannot influence or modify these inputs.

**Location**: `sbu-legal-engine`
**Endpoint**: `POST /upload`
**Mechanism**:
1.  **Ingest**: File binary received by Engine.
2.  **Parse**: `pdf-lib` extracts the precise page count (`pageCount`).
3.  **Hash**: `SHA-256` computes the cryptographic identity of the content (`complexityHash`).
4.  **Manifest**: The Engine signs a `CostManifest` (JWT) containing `jobId`, `pageCount`, and `complexityHash`.
5.  **Output**: The `CostManifest` is returned to the client. This token is the only accepted input for pricing. **It does not grant execution authority.**

## 4. COST FREEZE & BINDING
Pricing logic is applied deterministically by the Gateway validation layer, strictly adhering to the signed `CostManifest`.

**Location**: `sbu-legal-gateway`
**Endpoint**: `POST /checkout/quote` -> `POST /checkout/intent`
**Formula**:
```javascript
PRICE_CENTS = BASE_RATE (500) + (PAGE_COUNT * PER_PAGE_RATE (100))
```
**Process**:
1.  **Quote**: Gateway verifies the `CostManifest` signature. Calculates `priceCents`. Returns `SignedQuote` (JWT).
2.  **Intent**: Gateway verifies `SignedQuote`. Creates a Stripe `PaymentIntent` with `capture_method: 'manual'` (Authorization Hold).
3.  **Binding**: The Gateway locks the transaction parameters into Stripe Metadata:
    *   `jobId`: Target Engine instance.
    *   `complexityHash`: Content identity.
    *   `draftType`: Execution mode.
    *   `quoteHash`: Audit trail.

The cost is frozen. Modifying the file generates a new hash/ID, invalidating the quote.

## 5. PAYMENT & AUTHORITY (RUBICON)
Authority is granted only upon cryptographic confirmation of payment settlement.

**Location**: `sbu-legal-gateway`
**Endpoint**: `POST /checkout/finalize`
**Mechanism**:
1.  **Settlement**: Stripe processes the payment method. Status becomes `requires_capture` (Authorization Hold).
2.  **Validation**: Gateway retrieves the `PaymentIntent`.
3.  **Cross-Check**: Verifies `amount` matches the signed expectation and metadata binding.
4.  **Issuance**: Gateway mints a single-use `ExecutionToken` (JWT).
    *   **Scope**: `EXECUTE_IRREVERSIBLE`
    *   **Subject**: `jobId`
    *   **State**: The Gateway does not store this token. It is stateless.

## 6. POST-AUTHORITY EXECUTION CONSTRAINTS
Once authorized, execution is strictly bounded by hard resource limits enforced by the Engine.

**Location**: `sbu-legal-engine`
**Endpoint**: `POST /generate`
**Limits**:
*   **Max Output Tokens**: `8192` (Hard Limit in `generationConfig`).
*   **Temperature**: `0.0` (Deterministic).
*   **Pipeline Steps**: `1` (Atomic generation).
*   **Execution Time**: Worker Global Timeout (approx. 30s-60s).

## 7. SINGLE-USE ENFORCEMENT
The Engine Durable Object is the final authority on state. It acts as a one-way latch.

**Location**: `sbu-legal-engine`
**Endpoint**: `POST /acquire_authority`
**Mechanism**:
1.  **Verification**: Engine verifies the `ExecutionToken` signature (Gateway Secret).
2.  **Check**: Inspects internal `authorityState`.
3.  **Guard**:
    *   If `POST_AUTHORITY`: **HARD REJECT (409 Conflict)**.
    *   If `PRE_AUTHORITY`: Proceed.
4.  **Transition**: Atomically updates `authorityState` to `POST_AUTHORITY`. This is irreversible.

## 8. FAILURE & INCINERATION SEMANTICS
The system adheres to a "Cash Transaction" model. Failure results in total loss of the session state.

**Condition**:
*   LLM Generation Failure (after internal provider retries; session retries are prohibited).
*   Resource Exhaustion (`MAX_TOKENS` exceeded).
*   Security Violation (Token mismatch).
*   Timeout.

**Action (Incineration & Economic Latch)**:
1.  **Cancel Hold**: The Engine explicitly cancels the Stripe authorization hold (`stripe.paymentIntents.cancel()`).
2.  **Status**: `authorityState` explicitly marked `CONSUMED_FAILURE`.
3.  **Storage**: `state.storage.deleteAll()` invoked immediately.
4.  **Response**: `500 Internal Server Error`.
5.  **Recovery**: None. The `jobId` is burned. The user must restart (upload -> pay -> execute).

## 9. EXPLICIT NON-CONCEPTS
The following do not exist in the system architecture:
*   **User Accounts**: Identity is ephemeral to the session.
*   **Balances**: Every action is paid for individually in full.
*   **Refunds Logic**: Technical failures invoke incineration, not reversal.
*   **Draft Persistence**: Generation is fire-and-forget; results are ephemeral.

## 10. FINAL SYSTEM INVARIANTS
*   **One execution per payment.**
*   **Cost fixed before authority.**
*   **Authority consumed exactly once.**
*   **No retries.**
*   **Total incineration upon completion or failure.**
