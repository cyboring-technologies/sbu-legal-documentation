---
id: "README_ENGINE_V2"
title: "Engine V2 — Sovereign Continuous Engine"
type: "Core Architecture & Systems"
version: "v2.0"
last_updated: "2026-03-07"
status: "Approved"
---

# Engine V2 — Sovereign Continuous Engine

**Context:** *The core architectural document for the Engine. It defines the "One-Shot" invariant, stating that the engine mounts once, runs continuously, allows no retries, and incinerates all data.*

STATUS: NORMATIVE
ROLE: Core Execution Engine · Single Source of Truth (V2)
SCOPE: End-to-End Execution (Pre-Authority + Post-Authority)
AUTHORITY: Architectural & Operational
VERSION: Engine V2
SUPERSEDES: README_ENGINE.md (V1 — Legacy, As-Built)

1. Purpose & Definition

Engine V2 is a single, sovereign, continuous execution engine that governs the entire lifecycle of a document processing session, from initial document ingestion to final incineration.

The Engine is mounted once per session, runs inside a single uninterrupted runtime, and never hands execution to an alternate engine, surface, or context.

There is no concept of “pre-engine” or “post-engine”.
There is only one Engine, operating under different authority states.

2. Fundamental Invariants (Non-Negotiable)

The following invariants define Engine V2. Any implementation that violates them is incorrect by definition.

Single Engine per Session
Exactly one Engine instance exists from entry to termination.

Single Runtime
No remount, rehydration, route-based engine swap, or context reset is permitted.

Authority ≠ Surface
Payment changes authority, not UI, layout, routing, or runtime identity.

One Rubicon
Irreversibility occurs exactly once, at payment confirmation.

One-Shot Execution
Each session produces at most one final draft.

Total Incineration
All session data is destroyed at termination with no persistence.

3. Entry Contract

A user action (CTA) opens directly into Engine V2.

No intermediate execution surface exists.

The Engine:

occupies the full viewport,

establishes its own layout and providers,

and remains mounted for the entire session.

From this point onward, all user interaction occurs inside the Engine.

### 3.1 Handover Invariants (One-Shot Handover)

The transition from Landing to Engine complies with the **One-Shot Ephemeral Theme Handover Pattern**.

*   **Theme Propagation**: Current UI theme (`light` | `dark`) is passed via `?theme=` query parameter.
*   **Language Propagation**: Current UI locale is passed via `?lang=` query parameter.
*   **Technical Neutrality**: The Engine must apply the received theme and language before the first meaningful paint to maintain perceptual continuity without persistent synchronization.

### 3.2 Entry Routing Normalization (v2.1)

To ensure deployment flexibility and technical sovereignty, the Engine router is **Path-Agnostic**.

*   All endpoints (e.g., `/init`, `/upload`, `/execute`) are available both at the root `/` and under the `/engine/` prefix.
*   The root entry point (`/`) and `/engine/` both serve the sovereign client UI.
*   This allows the Landing Page to mount the Engine using a standardized `/engine/` path invariant regardless of the underlying CDN or worker routing configuration.

4. Authority Model

Engine V2 operates under a binary authority model.

4.1 Pre-Authority State (Reversible)

This is the default initial state.

In this state, the Engine MAY:

Accept document uploads, protected by a **Dual-Layer Structural Validation Gate** (frontend word/char count and backend buffer scanning) that rejects empty or unprocessable scanned documents before generating a Cost Manifest.

Render document preview.

Accept attorney-supplied supplemental facts via the controlled fact channel (`TRUSTED_STRATEGIC_CONTEXT`). This field is RAM-only, optional, and forwarded to the prompt at Rubicon crossing. It does not alter the authority model or introduce a new phase.

In this state, the Engine MUST NOT:

Generate final drafts.

Execute irreversible transformations.

Emit final downloadable artifacts.

Persist any state outside volatile memory.

Consume execution tokens.

All state is ephemeral, reversible, and memory-resident.

4.2 Payment Rubicon (Authority Acquisition)

The Rubicon is crossed when the user explicitly confirms intent to generate the draft and completes payment.

At this instant:

The Gateway activates exclusively as an authority validator.

Payment is validated.

A single-use execution token is issued.

The Engine transitions to Post-Authority.

Hard rules:

The Engine is not remounted.

The UI does not change.

No layout, route, or provider is altered.

Only authority state changes.

### Rubicon Atomicity (Current Implementation)

The execution authority is emitted and consumed atomically
inside `/execute_after_payment`.

There is no polling.
There is no POST_AUTHORITY passive state.
There is no intermediate confirmation.
Payment authorization (Hold) triggers irreversible generation.
If draft passes structural integrity, the Engine explicitly calls `stripe.paymentIntents.capture()`.
If generation or validation fails, it calls `stripe.paymentIntents.cancel()`.

4.3 Post-Authority State (Irreversible · One-Shot)

After the Rubicon:

Document is frozen.

The Engine generates the draft exactly once. The Engine enforces a closed deductive legal structure (Fact → Rule → Subsumption → Consequence) for legally operative claims.

The user may:

review,

submit one final, formal amendment (which permanently locks into the UI as an uneditable historical record),

approve the draft.

Final download is enabled.

No retries, resets, or re-execution are permitted.

5. Data Model & Persistence

All session data lives only in volatile memory.

No document or draft is persisted to:

databases,

object storage,

logs,

analytics systems.

The value of the system is entirely contained in the final downloaded artifact.

6. Termination & Incineration

Termination occurs immediately after final approval and download, or upon explicit abandonment or failure.

Termination sequence:

All in-memory state is destroyed.

Execution token is invalidated.

Gateway authority is closed.

Engine is unmounted.

User is redirected to the homepage.

There is no recovery path.

7. What Engine V2 Is NOT

Engine V2 is explicitly not:

A SaaS application.

A multi-session workspace.

A user account system.

A document history service.

A resumable workflow.

A background processing system.

Any proposal introducing these properties violates this contract.

8. Governance & Change Rules

This document defines Engine V2 as intended and enforced architecture.

Edits are permitted only if:

Engine V2 behavior changes in production, and

The change is already live in code, and

The edit documents reality, not intent.

If Engine V2 is not yet live, this document governs all future implementation work.

9. Supersession Notice

README_ENGINE.md (V1) remains valid only for the legacy system currently in production.

Upon V2 deployment:

V1 is deprecated.

This document becomes the sole Engine authority.

10. Final Rule

There is exactly one Engine.
It runs once.
It becomes irreversible once.
And it leaves nothing behind.