---
id: "README_GATEWAY_V2"
title: "Gateway V2 — Post-Payment Authority Switch"
type: "Core Architecture & Systems"
version: "v2.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Gateway V2 — Post-Payment Authority Switch

**Context:** *Defines the Gateway's role as a stateless authority switch. It clarifies that the Gateway never hosts UI or starts sessions; it only validates payment and issues the authority token.*

STATUS: NORMATIVE
ROLE: Authority Validation · Irreversibility Guard
SCOPE: Payment Rubicon & Post-Authority Execution
AUTHORITY: Architectural & Operational
VERSION: Gateway V2
SUPERSEDES: README_GATEWAY.md (V1 — Legacy, As-Built)

1. Purpose & Definition

Gateway V2 is an authority-only component whose sole responsibility is to validate payment-derived authority and enable the irreversible one-shot execution of the Engine.

The Gateway is not an entry surface, not a user interface, and not an execution environment.

It exists exclusively to:

validate post-payment authority,

issue or validate a single-use execution token,

guard the Rubicon of irreversibility.

2. Core Principle (Non-Negotiable)

The Gateway does not start the Engine.
The Engine already exists.
The Gateway only changes what the Engine is allowed to do.

Any design where the Gateway:

mounts the Engine,

hosts UI,

defines layout,

or acts as a pre-execution surface
violates this contract.

3. Position in the System

The Engine V2:

mounts at session start,

runs continuously,

operates pre-authority and post-authority.

The Gateway V2:

remains dormant until payment is initiated,

activates only at the Rubicon,

never owns runtime, UI, or state beyond authority.

The Gateway is a logical syscall, not a phase.

4. Authority Instrument — Execution Token

Gateway V2 governs a single instrument of authority:

Execution Token (V2)

Opaque: No business semantics.

Single-Use: Valid for exactly one irreversible execution.

Short TTL: Strict expiration window.

Volatile: Never persisted to disk or database.

Non-Identifying: Authorizes execution, not a user.

The token is:

issued or validated only after successful payment,

consumed exactly once,

immediately invalidated after use.

5. Payment Rubicon Responsibilities

The Rubicon occurs when the user confirms intent to generate the draft and authorizes the payment hold (`capture_method: 'manual'`).

At that instant, Gateway V2 MUST:

Validate successful payment.

Issue or validate a fresh execution token.

Signal the Engine that authority is granted.

Enforce that authority can be consumed only once.

Gateway V2 MUST NOT:

alter the UI,

trigger a re-render or remount,

redirect to a new execution surface,

persist payment or execution data.

6. Gateway ↔ Engine Contract
Gateway Obligations

Validate authority at the moment of irreversible execution.

Enforce single-use semantics.

Invalidate authority after completion or failure.

Remain stateless beyond volatile memory.

Engine Obligations

Refuse any irreversible action without valid authority.

Treat authority as binary (absent / present).

Consume authority exactly once.

Trigger incineration upon completion.

7. Lifecycle States (Gateway Perspective)

Gateway V2 exposes no user-visible UI states.
Its internal lifecycle is purely logical:

State	Meaning
DORMANT	No payment initiated. No authority exists.
ARMED	Payment in progress; authority pending.
AUTHORIZED	Valid execution token issued.
CONSUMED	Token used; execution in progress or completed.
INVALIDATED	Token destroyed; Gateway closed.
8. Failure Handling & Incineration

Any failure after authorization:

invalidates the token,

forces Engine termination,

triggers full incineration.

No retries are allowed.

Any retry requires a new payment and a new authority cycle.

Failure does not create partial authority.

9. What Gateway V2 Is NOT

Gateway V2 is explicitly not:

A login system.

An authentication provider.

A session manager.

A UI surface.

A routing mechanism.

A persistence layer.

A retry controller.

Any attempt to extend the Gateway beyond authority enforcement violates this contract.

10. Governance & Change Rules

This document defines Gateway V2 as intended and enforced architecture.

Edits are permitted only if:

Gateway V2 behavior changes in production, and

The change is already reflected in code, and

The edit documents reality, not intent.

Until V2 is live, this document governs all Gateway implementation work.

11. Supersession Notice

README_GATEWAY.md (V1) remains valid only for the legacy system.

Upon deployment of Engine V2:

Gateway V1 is deprecated.

This document becomes the sole Gateway authority.

12. Final Rule

The Gateway does not execute value or capture funds.
It authorizes destruction.
And it exists for a single moment only.