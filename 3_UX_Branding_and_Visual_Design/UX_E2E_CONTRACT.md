---
id: "UX_E2E_CONTRACT"
title: "Sovereign End-to-End UX Governance Contract"
type: "UX, Branding & Visual Design"
version: "v1.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Sovereign End-to-End UX Governance Contract

**Context:** *Governs the end-to-end user experience to enforce the "One-Shot" mental model. It prohibits UX patterns like "save for later," "create account," or "dashboard."*

**STATUS:** NORMATIVE · AUTHORITATIVE
**ROLE:** UX Meaning · Perception · Experience Governance
**SCOPE:** End-to-End User Experience (Landing → Engine → Incineration)
**SSoT FOR:** Copy · Microcopy · Flows · Perceptual Model
**SUBORDINATE TO:**

* `SBU_legal_business_axioms.md`
* `BASE_EXECUTION_CONTRACT.md`
* `README_ENGINE_V2.md`
* `README_GATEWAY_V2.md`
* `ENGINE_VISUAL_CONTRACT.md`

In case of conflict, **Business Axioms and contracts prevail V2**.

---

## 0. Guiding Principle (UX Invariant)

The user **does not use a system**.

The user **performs an irreversible act**.

Any experience that suggests:

* continuity
* recurring use
* safe exploration
* testing
* return

**violates this contract.**

---

## 1. E2E UX States (Single Canon)

There are **only** the following UX states:

1. **Pre-Contact (Landing)**
2. **Engine Mounted**
3. **Pre-Authority (Reversible)**
4. **Payment Rubicon (Authority)**
5. **Post-Authority (Irreversible)**
6. **Closure**
7. **Incineration**

There are no additional perceptual sub-states.

---

## 2. Stage 1 — Pre-Contact (Landing)

### What the user understands

* There is a system that **generates a specific legal document**.

* The system **is not a continuous service**.

### What they think they are doing

* Evaluating whether they want to **perform** that action.

### Valid expectations

* Clarity about the **purpose**.

* Understanding of the **one-shot**.

* Understanding of the **irreversibility**.

### Expectations to explicitly deny

* Saving.

* Retries.

* History.

* Account.

* "I'll finish it later."

### Permitted emotions

* Clarity.

* Seriousness.

* Decision.

### Prohibited emotions

* Playful curiosity.

* Feeling like they are in a sandbox.

* Exploration without consequences.

### Binary Test

> Could the user think that "it will come back later"?

* Yes → **FAIL**
* No → **PASS**

---

## 3. State 2 — Engine Mounted

### UX Definition

The Engine **is not presented**.

The Engine **is already there**.

### Perceptual Rules

* No welcome message.

* No onboarding.

* No system explanation.

* No "start" indicator.

### Correct Mental Model

> "I am inside the running system."

### Unacceptable UX Error

Any transition signal like:

* "Step 1"
* "Start"
* "Configure your document"

---

## 4. State 3 — Pre-Authority (Reversible)

### What the user understands

* They are preparing **conditions**.

* They haven't **executed** yet.

### What they think they are doing

* Defining the parameters of the action.

### The Upload Structural Gate (UI-1)

* Before passing to UI-2, the system acts as a rigid, institutional gate.
* If a document is empty or a scanned image lacking digital text, it is **rejected instantly** pre-upload.
* There is no quote gracefully generated for garbage. The upload stops dead. This reinforces the perception of the Engine as a strict machine, not a forgiving web form.

### Valid expectations

* They can correct.

* They can abandon without consequences.

### Expectations to negate

* Preview of the final result.

* Simulation of the final document.

* "Example" of the output.

### Hard rule

Nothing should resemble:

* a demo
* a final preview
* an actual draft

### Permitted emotions

* Control.

* Precision.

* Responsibility.

### Forbidden Emotions

* Play.

* Experimentation.

* "Let's see what happens."

### Binary Test

> Could the user believe they have already obtained value?

* Yes → **FAIL**
* No → **PASS**

---

## 5. Stage 4 — Payment Rubicon (Authority)

### UX Definition

Payment **is not a purchase**.

Payment is a **crossing of irreversibility**.

### Absolute Rules

* No visual change to the Engine.

* No "proceed to checkout."

* No sense of a new phase.

### What the user understands

* They are **authorizing** an irreversible act.

* There is no going back.

### What they should NOT understand

* That they are buying access.

* That they can repeat the process.

* That they are starting a relationship.

### Dominant Emotion

* Aware Gravity

### Critical UX Error

Payment Celebration → **Immediate FAIL**

---

## 6. State 5 — Post-Authority (Irreversible)

### What the User Understands

* The act **has already occurred**.

* The system now **responds**, not asks.

### Valid Expectations

* Review.

* Submit a single, final refinement (Amendment Event).

**Crucial "Refine" UX Constraints:**
  * Inputs must freeze instantly upon submission (like Pre-Authority inputs).
  * The refinement instruction must permanently display as an uneditable factual record (e.g., "Enmienda Aplicada").
  * All refinement buttons must be completely removed from the DOM post-submission, leaving no "second chance" UI affordances.

* Approve or reject.

### Negated Expectations

* Re-execute.

* Change baseline inputs.

* "Start over".

### UX Rule

The UI **does not become friendlier** after payment.

### Permitted Emotions

* Sobriety.

* Focus.

* Purpose.

### Binary Test

> Is there any sign of a "second chance"?

* Yes → **FAIL**
* No → **PASS**

---

## 7. State 6 — Closure

### Definition

Closure occurs **at final approval**.

### Mandatory UX

* Immediate download.

* No continuation message.

* No "what's next".

### Prohibitions

* "Thank you for using…"
* "Come back anytime"
* "Your document will be available…"

---

## 8. State 7 — Incineration

### Perceptual Definition

Destruction **must be understood**, not decorated.

### Rules

* Explicit incineration.

* No ambiguity.

* No romanticizing.

### Correct Mental Model

> "This is over. There's nothing left here."

### Critical UX Error

Leaving doubt about persistence → **Total FAIL**

---

## 9. UX Promises

### Explicit Promises Allowed

* One document.

* One execution.

* Total incineration.

### Implicit Promises Allowed

* Correctness.

* Containment.

* Neutrality.

### Forbidden Promises

* Continuity.

* Relationship.

* Platform.

* Service.

---

## 10. Semantic Boundaries (Firewall)

### Forbidden Words/Frames

* platform
* app
* account
* history
* save
* back
* future session
* workspace
* project
* test
* demo

Use of any → breach of contract.

---

## 11. Unacceptable UX Errors (Blacklist)

* Feeling like a "recurring user."

* Feeling like an "active customer."

* Feeling like they're "on trial."

* Feeling "safe to experiment."

* Feeling "supported."

---

## 12. Global Binary Tests

### Can the user describe the system as "software I use"?

* Yes → **FAIL**

### Can they describe the payment as "buying access"?

* Yes → **FAIL**

### Can they believe that something is saved?

* Yes → **FAIL**

### Can they visually identify when the payment occurred without seeing it?

* Yes → **FAIL**

---

## 13. Governance Rule

This contract:

* blocks copy, microcopy, marketing, and workflows.

* cannot be reinterpreted.

* cannot be softened.

Any output that violates this:

* is considered incorrect,

* is blocked,

* is discarded.

---

## 14. Final UX Axiom

The system doesn't support.

It doesn't teach.

It doesn't retain.

It executes.

And disappears.

UX_E2E_CONTRACT.md — SEALED
