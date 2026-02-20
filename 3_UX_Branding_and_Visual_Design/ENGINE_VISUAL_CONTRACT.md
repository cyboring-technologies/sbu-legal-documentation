---
id: "ENGINE_VISUAL_CONTRACT"
title: "Engine Visual Contract"
type: "UX, Branding & Visual Design"
version: "v1.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Engine Visual Contract

**Context:** *Strictly governs how the Engine is rendered. It mandates full viewport sovereignty and prohibits enclosing the Engine in modals or containers, ensuring it feels like a distinct runtime.*


> **STATUS:** NORMATIVE
> **ROLE:** Visual Governance & UX Architecture
> **HIERARCHY:** Subordinate to [README_ENGINE.md](./README_ENGINE.md)
> **LAST VERIFIED AGAINST CODE:** 2026-02-03
> **VERIFIED FILES:**
> - `src/components/payment/CheckoutFlow.tsx`
> - `src/components/execution/ExecutionView.tsx`
> - `src/app/[locale]/page.tsx`
> - `src/app/layout.tsx`

---

## 1. Purpose & Scope

**Purpose:**
This document strictly defines the visual rendering behavior of the "Engine" (Execution Environment). It acts as a firewall between marketing aesthetics and operational utility.

**Scope:**
This contract governs:
*   The `ExecutionView` component and its parent containers.
*   The transition mechanism from "Landing" to "Engine".
*   The viewport properties during the Execution Phase.

**Out of Scope:**
*   Landing Page design.
*   Pre-Execution "Checkout/Estimation" flows (CTA-1).
*   Pricing logic or copy.
*   Internal Engine logic (governed by `README_ENGINE.md`).

---

## 2. Engine Rendering Mode (Hard Rules)

The following rules are **binary prohibitions**. Any deviation is a bug.

### Rule 2.1: Full Viewport Sovereignty
*   The Engine **MUST** occupy the entire viewport (`100vw` × `100vh`) or the substantial equivalent reserved for a top-level application view.
*   The Engine **MUST NOT** share screen real estate with marketing headers, footers, or sidebars.

### Rule 2.2: Prohibition of Containment
The Engine **MUST NOT** be rendered within:
*   ❌ Modals or Dialogs.
*   ❌ Drawers or Slide-overs.
*   ❌ Cards or "floating" surfaces.
*   ❌ Constrained containers (e.g., `max-w-lg`, `container`, `mx-auto` with width limits).

### Rule 2.3: Layout Independence
*   The Engine **MUST NOT** inherit the grid, typography scale, or layout constraints of the marketing site.
*   The Engine establishes its own coordinate system rooted in the viewport edges.

### Rule 2.4: Mode-Based Transition
*   The transition to the Engine is a **Mode Change**, functionally equivalent to a route change.
*   It **MUST NOT** be presented as a "step" in a multi-step form on the Landing Page.

---

## 3. Visual Semantics

The Engine visually communicates **utility, precision, and neutrality**.

*   **Aesthetics**: Minimalist, high-contrast structural differentiation.
*   **Hierarchy**: Functional (Structure > Source > Draft).
*   **State Visibility**: Technical states (UPLOADING, ANALYZING, INCINERATED) are displayed raw, without marketing euphemisms.
*   **Absence**: No persuasive copy, no upsell banners, no "delight" animations unrelated to system state.

---

## 4. Integration with Unified SPA (Explicit Boundary)

While the Engine shares the React runtime (SPA) with the Landing Page:

*   **Visual Isolation**: The Engine must feel like a distinct application launching.
*   **Route/State Sovereignty**: The Engine's state must not be accidentally destroyed by Landing Page interactions (e.g., closing a modal).

---

## 5. Current Compliance Status (Code-Verified)

**Verification Date:** 2026-02-03
**Inspector:** Antigravity

| Rule | Status | Violation Detail |
| :--- | :--- | :--- |
| **2.1 Full Viewport** | ✅ **COMPLIANT** | `ExecutionView` uses `w-full h-full` in `fixed w-screen h-screen` container. |
| **2.2 No Modals** | ✅ **COMPLIANT** | Engine is rendered at root level, exclusive of Landing Layout and Modals. |
| **2.3 No Constraints** | ✅ **COMPLIANT** | No `max-w` or `mx-auto` constraints on the Execution Mode container. |
| **2.4 Mode Change** | ✅ **COMPLIANT** | Implemented `executionSession` state switching. Landing Page is unmounted/hidden during execution. |
| **3. Visual Semantics** | ✅ **COMPLIANT** | `ExecutionView` uses functional grid layout and minimal aesthetics. |

**Critical Violations caused by:**
*   **None** - Codebase is compliant.

---

## 6. Enforcement Rule

Any Code Change Request (PR) that introduces or maintains:
1.  A modal wrapper around `<ExecutionView />` or its parents.
2.  A `max-w` constraint on the active Engine view.
3.  A shared layout with the Landing Page marketing content.

**MUST BE REJECTED** as a violation of this Core Contract. Use this document to block such regressions.
