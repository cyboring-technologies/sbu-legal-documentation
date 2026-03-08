---
id: "BASE_EXECUTION_CONTRACT"
title: "Single Sovereign Engine — Base Execution Contract"
type: "Execution Principles & Token Models"
version: "v2.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Single Sovereign Engine — Base Execution Contract

**Context:** *Defines the fundamental execution model: a single sovereign engine that runs once per session. It establishes the "Rubicon" concept where payment triggers a one-way transition to an irreversible authority state.*


STATUS: NORMATIVE
ROLE: Primary source of architectural truth
OBJECTIVE: To define the only valid execution model for the system

GOVERNANCE NOTE

This project is governed by a closed set of contracts.
If a document is not listed here, it has no authority.
Legacy and as-built documents are historical only.
Do not reconcile or merge them with V2 contracts.

---

## 1. Engine Definition

The system is structured around a single sovereign Engine, which constitutes the sole surface of execution, interaction, and value.

There are no external phases, alternative engines, or surfaces prior to or subsequent to this Engine.

The Engine is mounted only once per session and runs in a continuous, uninterrupted, and sovereign runtime, from the beginning to the final completion of execution.

---

## 2. System Entry

Clicking the CTA directly opens the Engine.

There are no intermediate surfaces.

The Engine:

occupies the entire viewport,

establishes its own layout tree,

defines its own lifecycle,

and does not inherit any external visual or structural context.

From this point forward, everything happens within the same Engine.

3. Pre-Authority State (Reversible)

Before payment, the Engine operates in reversible mode, without irreversible authority or token consumption.

In this state, the Engine CAN:

Allow document upload.

Display document preview.

Perform structural parsing.



In this state, the Engine CANNOT:

Generate final drafts.

Execute irreversible processes.

Issue final downloadable artifacts.

Persist information outside of volatile memory.

Consume authority or tokens.

The entire state resides exclusively in the Engine's memory and is completely disposable.

---

## 4. Payment Event — The Rubicon

The system's only point of irreversibility occurs when the client explicitly confirms their intention to generate the draft and completes the payment.

At that exact moment:

The Gateway is activated exclusively as an authority mechanism.

The payment is validated.

A one-shot execution token is issued.

The Engine crosses the Rubicon and enters an irreversible state.

This event does NOT:

mount a new Engine,

change the route,

restart the runtime,

re-render the tree,

or alter the visual context.

The Engine remains identical; only its authority state changes.

5. Post-Authority (One-Shot) State

After payment, the Engine operates in irreversible one-shot mode.

In this state:

The existing document in memory is frozen.

The Engine generates the draft.

The client can:

edit (locally/temporarily, if applicable),

submit a formal, singular amendment (a locked, visible "Enmienda Aplicada" event),

approve the result.

The Engine enables the final document download.

*Note on LLM Stabilization:* Internal systemic provider retries (e.g., trying GPT-5.3 multiple times or falling back to Gemini due to API timeouts) are strictly considered intra-runtime operations. They do not constitute session extensions or re-executions, as long as the user only perceives and interacts with a single final generated draft.

There is no:

repetition,

restart,

re-execution,

or session extension.

---

## 6. Closure and Incineration

After approval and final download:

The session is completely incinerated:

original document,

draft,

internal Engine state.

The token is permanently invalidated.

The Gateway is closed.

The Engine is dismantled.

The client is redirected to the homepage.

There is no recovery, history, or subsequent persistence.

---

## 7. Non-Negotiable Principles

One Engine per session.

One continuous runtime.

Payment changes authority, not surface.

Irreversibility occurs only once.

Every execution is one-shot.

Every session ends in incineration.

---

## 8. Final Rule

Any implementation that introduces:

multiple engines,

multiple runtimes,

perceptual transitions,

or out-of-memory persistence
violates this contract and must be considered incorrect by definition.