---
id: "INDEX"
title: "Documentation Index for SBU-Legal"
type: "Meta Documentation"
version: "v1.0"
last_updated: "2026-03-21"
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
    *   *Update (2026-03-08): Implemented the Primary LLM Stabilization Layer using `gpt-4o` as primary and `gemini-2.0-flash` as sequential fallback, configuring timeouts and automatic internal retries that do not violate the One-Shot Execution contract. (Note: initially documented as GPT-5.3 / Gemini 3.1 Pro — corrected 2026-03-08 after those model IDs were confirmed non-existent by API 404 responses; production code updated accordingly.)*
    *   *Update (2026-03-10): Successfully deployed Engine Worker to production at `engine.documentos.legal`. Confirmed production secrets for OpenAI, Gemini, and Stripe.*
    *   *Update (2026-03-10): Implemented Bootstrap Configuration & Origin Injection (v2.2), resolving a critical initialization failure by dynamically injecting service origins (Gateway/Landing) from the Worker environment into the frontend, eliminating hardcoded local development URLs.*
    *   *Update (2026-03-11): Added safe HTTP HEAD support to the Engine Worker to fulfill infrastructure health checks and crawler probes without triggering execution or DO state.*
    *   *Update (2026-03-11): Investigated and corrected `STRIPE_PUBLISHABLE_KEY` environment misconfiguration, ensuring persistent secret injection via Wrangler for successful front-end initialized Stripe Elements.*
    *   *Update (2026-03-11): Fixed a post-incineration 404 routing error by replacing the relative redirect path with a strictly governed `LANDING_ORIGIN` template literal to ensure users are safely returned to the landing domain.*
    *   *Update (2026-03-12): Performed OpenAI API account identity audit. Confirmed production key (suffix `eL6PQA`) is active and authorized for 105 models, but currently limited by account credits (429 status verified).*
    *   *Update (2026-03-18): Finalized production-ready state by removing all `[DEBUG]` logs. Enforced strict Stripe environment immutability via `stripe-infrastructure/shared/stripeConfig.js` and confirmed `SESSION_SECRET` consistency across runtimes.*
    *   *Update (2026-03-18): Implemented R2 Streaming Ingestion (v2.3). Resolved 500 errors on large uploads by removing `formData` parsing. Files are now streamed directly to R2; Durable Objects store only session metadata (`objectKey`, `extractedText`). Enforced strict incineration of R2 objects upon session completion or failure.*
    *   *Update (2026-03-19): Hardened document ingestion protocol. Resolved HTTP 431 and ISO-8859-1 encoding errors. Fixed a critical `ReferenceError` in `/execute_after_payment`. Successfully rolled out Engine v2.3 and Gateway v2.3 to production. Resolved a 500 initialization error by enforcing `STRIPE_ENV_MODE` and relaxing the strict `_LIVE` suffix requirement for legacy secrets in `stripeConfig.js`.*

*   **README_GATEWAY_V2.md**
    Defines the Gateway's role as a stateless authority switch. It clarifies that the Gateway never hosts UI or starts sessions; it only validates payment and issues the authority token for the already-running Engine.
    *   *Update (2026-03-11): Patched Gateway runtime to enforce strict `SESSION_SECRET` environmental presence before execution and implemented dynamic CORS validation supporting `Authorization` headers for Stripe Elements compatibility.*
    *   *Update (2026-03-11): Finalized production deployment to `gateway.documentos.legal`, injecting `STRIPE_SECRET_KEY` and `STRIPE_WEBHOOK_SECRET` via Wrangler, and verified active intercept of the Stripe webhook endpoint (`/webhook`).*
    *   *Update (2026-03-18): Implemented strict environment immutability. Isolated Gateway Node runtime from `process.env` by explicit `.dev.vars` parsing and enforced single-source-of-truth `env` pattern in `stripe-infrastructure/shared/stripeConfig.js`.*
    *   *Update (2026-03-19): Verified local Gateway connectivity via `http://localhost:8787` and synchronized shared Stripe logic imports. Successfully deployed Gateway v2.3 to `gateway.documentos.legal`, ensuring deterministic environment-specific key lookup via corrected `wrangler.toml` vars.*

*   **README_LANDING.md**
    Describes the Landing Page as a static marketing surface that informs users and links to the Engine. It explicitly states the landing page has no authority over execution, user state, or payments.
    *   *Update (2026-03-07): Added `/sitemap` HTML utility page (static, lists all pages + 24 AntiPages) and `generate-rss.mjs` post-build script producing `out/rss.xml` (4 blog items, RSS 2.0 + Atom self-link). Added `postbuild` npm hook to `package.json`. Corrected HTML sitemap `robots` directive from `noindex` to default `index, follow`. All changes are within the Landing SEO scope and do not affect Engine, Gateway, or execution contracts.*
    *   *Update (2026-03-10): Documented the `wrangler secret put` commands for production secrets: `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `OPENAI_API_KEY`, `GEMINI_API_KEY`, `SESSION_SECRET`.*
    *   *Update (2026-03-19): Synchronized environment variable naming. Added `NEXT_PUBLIC_ENGINE_ORIGIN` to `.env.local` to resolve hardcoded production fallbacks.*
    *   *Update (2026-03-21): Resolved critical sitemap 404 errors in production by localizing all sitemap and canonical URLs. Ensured `sitemap.ts` and `generateMetadata` include the mandatory locale prefix (`/es/` or `/en/`) to match the Static Export directory structure.*

*   **METADATA_EXTRACTION_ARCHITECTURE_V2.md** *(Deprecated — 2026-02-25)*
    Archived. Described the regex-based structural extraction pipeline (`Stage3Extractor.js`, `/extract`, `/review_metadata`, SHA-256 freeze, `<TRUSTED_CONTEXT>` injection). Fully removed during the Sovereign LLM migration (2026-02-25). The LLM is now the sole interpreter of source content. Retained for historical reference only.

*   **PROMPT_SYSTEM_STATE_V2.md**
    Documents the prompt engineering architecture. It uses a "Strict Envelope" model to segregate system instructions from user content to ensure structural integrity and prevent prompt injection or "bleed-through."
    *   *Update (2026-03-08): Added documentation for the Pre-Prompt Sanitization Layer (`sanitizeUntrustedSource`) which strips imperative control phrases from user documents before envelope assembly.*
    *   *Update (2026-03-08): Documented the addition of the Structural Imperative Neutralization Layer (`neutralizeImperatives`), expanding the pre-prompt defenses to safely break imperative authority semantics without altering legal document structure.*

*   **PROMPT_HARDENING_PHASE_1.md**
    A technical addendum recording the prompt hardening updates made in Phase 1 to improve legal density, mandate a closed deductive syllogism (Fact → Rule → Subsumption → Consequence), and eliminate pedagogical fluff.

*   **ENVIRONMENT_VARIABLES_REGISTRY.md**
    Centralizes the configuration registry of environment variables required for production and development deployments within the Cloudflare ecosystem.
    *   *Update (2026-03-18): Executed Phase 9 Hard Cut & Immutability Enforcement. Purged legacy config, strictly enforcing environment-specific keys and a deterministic, non-overridable `STRIPE_ENV_MODE` path with fail-fast invariants.*

*   **CLOUDFLARE_DEPLOYMENT_ARCHITECTURE.md**
    Details the serverless Cloudflare infrastructure, domain topology, and component deployment boundaries used by SBU-Legal.
    *   *Update (2026-03-10): Finalized Gateway Worker configuration and verified deployment status to `gateway.documentos.legal`.*
    *   *Update (2026-03-10): Finalized Engine Worker configuration and verified production deployment to `engine.documentos.legal`. Confirmed all Worker Routes and Durable Object bindings are operational.*
    *   *Update (2026-03-11): Documented manual `CNAME` to `workers.dev` requirement for Gateway DNS routing, replacing assumed auto-provisioning.*
    *   *Update (2026-03-18): Clarified Section 13 Deployment Workflow to explicitly state that Cloudflare Workers are deployed strictly via manual local `wrangler deploy` execution, while the Landing page utilizes native Cloudflare Pages Git integration. No GitHub Actions CI/CD pipelines are utilized.*
    *   *Update (2026-03-21): Implemented **Custom Domains** infrastructure fix. Migrated Engine and Gateway from legacy `routes` mapping to `custom_domain = true`, resolving intermittent TLS handshake failures and DNS 1001 errors during cold starts. Eliminated manual DNS CNAME requirements.*

*   **LOCAL_DEVELOPMENT_ENVIRONMENT_V1.md**
    Operational guide for initializing and running the SBU-Legal services locally. It defines the component directory structure, port mappings (3000/8787/8788), startup procedures, and Stripe CLI authentication workflow for developers using the binary located in `stripe-infrastructure/`.

## 2. Execution Principles & Token Models
*Documents that explicitly govern how the product is run, priced, and triggered upon payment.*

*   **BASE_EXECUTION_CONTRACT.md**
    Defines the fundamental execution model: a single sovereign engine that runs once per session. It establishes the "Rubicon" concept where payment triggers a one-way transition to an irreversible authority state.

*   **PRICING_EXECUTION_MODEL.md**
    Details the technical implementation of the pricing logic (`Base + Page Count`) and the authority transition. It describes how the `CostManifest` is signed and how payment validates the issuance of a single-use execution token.

*   **STRIPE_PAYMENT_FLOW.md**
    Defines the operational Stripe payment flow, the Rubicon event, and execution token issuance rules for crossing the payment boundary.
    *   *Update (2026-03-10): Verified production readiness of Gateway secrets and integration bindings during March 10 deployment audit.*
    *   *Update (2026-03-18): Finalized execution authority hardening. Implementation of strict environment immutability ensures that incorrect or mismatched Stripe keys cause a fatal crash before initialization, preventing any insecure fallbacks.*

## 3. UX, Branding & Visual Design
*Documents governing the visual identity, end-to-end user experience, and aesthetic constraints.*

*   **BRANDING_LANDING.md**
    Specifies the visual identity and UI standards for the landing page. It details the "Institutional Greyscale" color palette, typography (Inter/IBM Plex Sans), and component specifications (CTAs, Hero, Grid Patterns).
    *   *Update (2026-03-07): Inserted structural authority microcopy inside the homepage viewport, securing semantic context density.*
    *   *Update (2026-03-08): Localized the Authority Signal ("Motor de Tecnología Legal" / "Legal Technology Engine") to ensure bilingual coherence and SEO relevance across regions.*
    *   *Update (2026-03-21): Hardened and documented the `ctaType` architecture (v1.1). Corrected technical debt where `cta-2` was incorrectly used for navigational links instead of its intended role as a Security Modal trigger (now strictly enforced as a button element).*

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
    *   *Update (2026-03-21): Hardened AntiPage SEO and schema consistency. Universalized the inclusion of locale prefixes in canonical URLs and JSON-LD structured data (Service, Breadcrumb, FAQ), eliminating metadata mismatches between language variants.*

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