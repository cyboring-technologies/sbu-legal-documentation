---
id: "DOCUMENTATION_GOVERNANCE"
title: "Documentation Governance — Creation & Lifecycle Rules"
type: "Meta Documentation"
version: "v1.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Documentation Governance — Creation & Lifecycle Rules

**Context:** *This document defines the rules, standards, and life cycles for the creation and maintenance of SSoT (Single Source of Truth) documentation within the SBU-Legal architecture.*

---

This directory contains the Single Source of Truth for the SBU-Legal system. These documents act as absolute technical and business contracts. Any new implementation must comply with them, and any new document must follow the standards defined below.

## 1. Naming Standards

Every new documentation file must adhere to the following naming conventions:

1.  **Format (`UPPER_SNAKE_CASE`)**: All filenames must use capitalized letters separated by underscores (e.g., `BASE_EXECUTION_CONTRACT.md`). This conveys a strong, machine-readable, and engineering-focused tone.
2.  **No Redundancies**: Do not include prefixes like `SBU_LEGAL` or suffixes like `_SSOT`. The directory root itself establishes this context.
3.  **Standardized Versioning**: If a document specifies a particular architectural version, append the version number using `_V#` at the end of the filename (e.g., `README_ENGINE_V2.md`).
4.  **Descriptive Clarity**: Ensure the filename accurately reflects the document's operational purpose (e.g., `EXECUTIVE_SUMMARY_V1.md` instead of just `template.md`).

## 2. Header Block & Metadata

To ensure these rules act strictly as SSoT contracts and are easily parseable by tools, **every** document must begin with a standardized YAML front matter block, followed by the H1 Title and a `**Context:**` summary line.

### Required Header Template

```yaml
---
id: "[Upper-Snake-Case Identifier matching the filename, e.g., BRANDING_LANDING]"
title: "[Human-readable title, e.g., Landing Page Visual Identity and UX Standards]"
type: "[Category from the classification rules, e.g., UX, Branding & Visual Design]"
version: "[e.g., v1.0, v2.0]"
last_updated: "YYYY-MM-DD"
status: "[Draft / Proposed / Approved / Deprecated]"
---

# [Human-readable title, exact same as above]

**Context:** *A strict one-to-two sentence executive summary explaining what this document is, why it exists, and what system/rules it governs.*

---
```

## 3. Classification & Grouping Rules

When adding a new document, it must accurately fall under, and be placed within, one of the five core thematic directories inside the `Documentation/` folder. Ensure the document's `type` field in the metadata header matches the respective directory name.

*   **1_Core_Architecture_and_Systems**
    *   *Purpose*: Documents detailing technical implementations, core infrastructural components, Gateway logic, Engine setups, extraction, and SSoT system configurations.
*   **2_Execution_Principles_and_Token_Models**
    *   *Purpose*: Documents explicitly governing how the product runs, token models, pricing limits, and triggers upon payment (the Rubicon).
*   **3_UX_Branding_and_Visual_Design**
    *   *Purpose*: Documents governing visual identity, rendering rules, UI components, end-to-end user experience, and aesthetic/interaction constraints prohibiting recurring user perceptions.
*   **4_Business_Strategy_and_Economics**
    *   *Purpose*: Operational business plans, marketing strategies (GTM), revenue targets, launch validations, non-negotiable business rules, and unit economics.
*   **5_Meta_Documentation**
    *   *Purpose*: Organizational documentation, like `INDEX.md`, or this governance document itself, detailing how the directory is structured.

## 4. Operational Invariants for Documentation

*   **Subordination & Prevailing Context**: Always clarify at the top (under the context) if a document is subordinate to higher-level contracts (e.g., an implementation plan is subordinate to the `BASE_EXECUTION_CONTRACT.md`).
*   **Descriptive vs. Normative**: Always define within the text if the document is strictly *Normative* (a rule you must follow) or *Descriptive* (explaining how a peripheral system functions, such as the Landing Page).
*   **Deprecation Policy**: Never just delete a crucial historical contract. Instead, update the status to `status: "Deprecated"`, add a note indicating what document supersedes it, and mark the new active document as `status: "Approved"`.
