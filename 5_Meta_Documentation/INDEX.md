---
id: "INDEX"
title: "Documentation Index for SBU-Legal"
type: "Meta Documentation"
version: "v1.0"
last_updated: "2026-03-07"
status: "Approved"
---

# Documentation Index for SBU-Legal

**Context:** *The directory file summary for all SSoT documents, serving as a navigation guide organized by topic.*

This directory contains the Single Source of Truth (SSoT) documentation and other relevant documentation for the Strategic Business Unit-Legal, part of the Holding: Cyboring Technologies LLC, Delaware, USA. Below is a summary of each file, logically grouped by topic:

## 1. Core Architecture & Systems (READMEs & Architecture)
*Documents detailing the technical implementations, core components, and SSoT system configurations.*

    The core architectural document for the Engine. It defines the "One-Shot" invariant, stating that the engine mounts once, runs continuously, allows no retries, and incinerates all data upon completion or failure.
    *   *Update (2026-03-07): Formalized the Routing Normalization (v2.1) making the Engine path-agnostic and the One-Shot Ephemeral Theme Handover Pattern for perceptual continuity.*
    *   *Update (2026-03-08): Documented the Dual-Layer Pre-Authority Structural Validation Gate blocking empty or unprocessable scanned uploads.*
    *   *Update (2026-03-08): Documented the UI2 Editable Procedure functionality, defining how the frontend dynamically maintains the selector ephemerally and processed atomically at the Rubicon without requiring persistent DO overrides.*
    *   *Update (2026-03-08): Implemented the Primary LLM Stabilization Layer using GPT-5.3 as default and Gemini 3.1 Pro as sequential fallback, configuring timeouts and automatic internal retries that do not violate the One-Shot Execution contract.*

*   **README_GATEWAY_V2.md**
    Defines the Gateway's role as a stateless authority switch. It clarifies that the Gateway never hosts UI or starts sessions; it only validates payment and issues the authority token for the already-running Engine.

*   **README_LANDING.md**
    Describes the Landing Page as a static marketing surface that informs users and links to the Engine. It explicitly states the landing page has no authority over execution, user state, or payments.
    *   *Update (2026-03-07): Added `/sitemap` HTML utility page (static, lists all pages + 24 AntiPages) and `generate-rss.mjs` post-build script producing `out/rss.xml` (4 blog items, RSS 2.0 + Atom self-link). Added `postbuild` npm hook to `package.json`. Corrected HTML sitemap `robots` directive from `noindex` to default `index, follow`. All changes are within the Landing SEO scope and do not affect Engine, Gateway, or execution contracts.*


*   **METADATA_EXTRACTION_ARCHITECTURE_V2.md** *(Deprecated — 2026-02-25)*
    Archived. Described the regex-based structural extraction pipeline (`Stage3Extractor.js`, `/extract`, `/review_metadata`, SHA-256 freeze, `<TRUSTED_CONTEXT>` injection). Fully removed during the Sovereign LLM migration (2026-02-25). The LLM is now the sole interpreter of source content. Retained for historical reference only.

*   **PROMPT_SYSTEM_STATE_V2.md**
    Documents the prompt engineering architecture. It uses a "Strict Envelope" model to segregate system instructions from user content to ensure structural integrity and prevent prompt injection or "bleed-through."
    *   *Update (2026-03-08): Added documentation for the Pre-Prompt Sanitization Layer (`sanitizeUntrustedSource`) which strips imperative control phrases from user documents before envelope assembly.*
    *   *Update (2026-03-08): Documented the addition of the Structural Imperative Neutralization Layer (`neutralizeImperatives`), expanding the pre-prompt defenses to safely break imperative authority semantics without altering legal document structure.*

*   **PROMPT_HARDENING_PHASE_1.md**
    A technical addendum recording the prompt hardening updates made in Phase 1 to improve legal density, mandate a closed deductive syllogism (Fact → Rule → Subsumption → Consequence), and eliminate pedagogical fluff.

## 2. Execution Principles & Token Models
*Documents that explicitly govern how the product is run, priced, and triggered upon payment.*

*   **BASE_EXECUTION_CONTRACT.md**
    Defines the fundamental execution model: a single sovereign engine that runs once per session. It establishes the "Rubicon" concept where payment triggers a one-way transition to an irreversible authority state.

*   **PRICING_EXECUTION_MODEL.md**
    Details the technical implementation of the pricing logic (`Base + Page Count`) and the authority transition. It describes how the `CostManifest` is signed and how payment validates the issuance of a single-use execution token.

## 3. UX, Branding & Visual Design
*Documents governing the visual identity, end-to-end user experience, and aesthetic constraints.*

*   **BRANDING_LANDING.md**
    Specifies the visual identity and UI standards for the landing page. It details the "Institutional Greyscale" color palette, typography (Inter/IBM Plex Sans), and component specifications (CTAs, Hero, Grid Patterns).
    *   *Update (2026-03-07): Inserted structural authority microcopy inside the homepage viewport, securing semantic context density.*
    *   *Update (2026-03-08): Localized the Authority Signal ("Motor de Tecnología Legal" / "Legal Technology Engine") to ensure bilingual coherence and SEO relevance across regions.*

*   **ENGINE_VISUAL_CONTRACT.md**
    Strictly governs how the Engine is rendered. It mandates full viewport sovereignty (no headers/footers) and prohibits enclosing the Engine in modals or containers, ensuring it feels like a distinct runtime.

*   **UX_E2E_CONTRACT.md**
    Governs the end-to-end user experience to enforce the "One-Shot" mental model. It prohibits UX patterns like "save for later," "create account," or "dashboard," ensuring the user perceives the action as a single, irreversible event.
    *   *Update (2026-03-08): Explicitly codified the UI-1 Upload Structural Gate behavior. The Engine must reject garbage instantly to reinforce the strict institutional perception.*

*   **UX_NARRATIVE_JOURNEY.md**
    A chronological narrative documenting the end-to-end user journey from landing page CTA click to the ultimate incineration of the session. It describes the emotional tone, the mental model, and how the Sovereign Engine principles feel in practice to a client.
    *   *Update (2026-03-08): Added the in-line interactive procedure UI to the Pre-Authority section and detailed its strict structural removal during the Rubicon execution freeze.*

*   **ANTI_PAGES_TEMPLATE_CONTRACT_V1.md**
    Standard document that defines the structural, semantic, and technical architecture of AntiPages.
    *   *Update (2026-03-05): Added semantic SEO expansion, pricing transparency, and CTR headline optimization to `AntiPage.tsx` without violating structural block constraints.*
    *   *Update (2026-03-05): Restructured Next.js App Router sitemap generation in `src/app/sitemap.ts` to dynamically crawl and map all 24 Tier-A service variants from `antipages.json`.*
    *   *Update (2026-03-07): Standardized Title and Meta Description patterns for SERP conversions (Action + Document + Time) and injected targeted JSON-LD Structured Data models (Service/FAQ/Article) associating the 'documentos.legal' product to 'Cyboring Technologies LLC'.*
    *   *Update (2026-03-07): Validated indexing manifest injection and the systematic application of a deterministic internal crawl graph (4 dynamic links sorted by slug to ensure hydration compatibility) appended as the penultimate structural block.*
    *   *Update (2026-03-07): Added global Legal Layout Footer to `AntiPage.tsx` as a layout element rendered **after** the CTA block — outside the block template. Contains static links to `/legal/terms` (Términos de Servicio) and `/legal/privacy` (Política de Privacidad), plus "Cyboring Technologies LLC" attribution. Documented in Section 3 and Section 6 of this contract. Block order, CTA invariant, and `antipages.json` remain unmodified.*
    *   *Update (2026-03-07): Fixed critical static export errors by correcting `generateStaticParams` to include all 24 Tier-A slugs for both locales. Standardized internal navigation using localized `Link` components to prevent broken routing in the exported static site. Fixed AntiPage CTA logic to ensure proper routing and theme/language handover to the engine.*

## 4. Business Strategy, Marketing & Economics
*Documents defining the rules out in the market, launch numbers, and business propositions.*

*   **BUSINESS_AXIOMS.md**
    Establishes the non-negotiable business rules. It defines the product as a single irreversible execution (not a service or subscription) and prohibits any UX features that imply accounts, saving, or recurring use.

*   **EXECUTIVE_SUMMARY_V3_SBU_LEGAL.md**
    An operational executive summary of the business unit. It details the value proposition (immediate document generation), target audience (SMBs), and the "incineration" privacy model as a key selling point.

*   **ECONOMIC_LAUNCH_VALIDATION_REPORT.md**
    Analyzes the unit economics for the launch. It confirms that variable costs (Stripe fees + LLM tokens) are negligible relative to the ticket price ($6-$55), yielding gross margins above 90%.

*   **MARKETING_PLAN_V3.md**
    Outlines the structural SEO variant of the marketing plan. It focuses on replacing paid acquisition with high-intent procedural queries, utilizing a capitalized organic internal production base for delayed but autonomous returns.

*   **MARKETING_PARAMETRIC_MODEL.md**
    Defines the parametric marketing model and mathematical assumptions for SBU-Legal validation. It acts as an exploratory financial framework without establishing hardcoded limits, governing variables like SEO production, segmentation, and pricing.

*   **MARKETING_EXECUTION_FRAMEWORK_V1.md**
    Defines the operational unit economics, KPI framework, and test matrix required for commercial validation under the SBU-Legal constraint.

*   **ANTI_PAGES_MASTER_INVENTORY_V1.md**
    Structural document that maps the complete annual inventory of parametric landing pages (AntiPages). Establishes service-jurisdiction variants, tier prioritization, and serves as the source for `antipages.json`.

*   **sbu-legal-landing/src/messages/es.json**
    Contains all the copy of the landing page in Spanish (homepage, services, prices, about us, contact, FAQs, etc.). This acts as the definitive source for the website's marketing material and messaging.

## 5. Meta Documentation
*Documentation regarding the directory structure itself.*

*   **INDEX.md**
    This file. The directory file summary for all SSoT documents, serving as a navigation guide organized by topic.