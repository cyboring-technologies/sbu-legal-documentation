# ANTI-PAGES TEMPLATE CONTRACT V1

## 0. Status & Authority

This document is NORMATIVE, BLOCKING, and ARCHITECTURAL. It contains no final copy. Any AntiPage that violates the rules defined within this contract is invalid and must not be deployed.

---

## 1. Authority and Hierarchy

This document is strictly subordinate to:
* `BUSINESS_AXIOMS.md`
* `UX_E2E_CONTRACT.md`
* `README_LANDING.md`
* `ANTI_PAGES_MASTER_INVENTORY_V1.md`
* `ENGINE_VISUAL_CONTRACT.md`
* `PRICING_EXECUTION_MODEL.md`

This contract hereby declares:
* It is strictly subordinate to the Business Axioms.
* It cannot and will not introduce continuity.
* It cannot and will not modify the One-Shot model.
* It cannot and will not alter the single CTA to Engine.
* It cannot and will not introduce status, accounts, or persistence.

---

## 1. Architectural Principle

The underlying principle for all AntiPages is:
> Stable design. Variable content. Single engine.

The architecture strictly confirms the following rules:
* One single `AntiPage.tsx` file executes all pages.
* One single structural layout applies globally.
* Zero structural conditionals allowed per variant.
* Zero visual conditionals allowed per service or jurisdiction.

### Static Export Constraint

AntiPages must remain compatible with Next.js static export.

Prohibited:
- Server-side rendering dependencies
- Runtime data fetching
- API-driven content injection
- Dynamic route resolution outside generateStaticParams()

All AntiPages must be fully renderable at build time.

---

## 2. Data Layer Contract (`antipages.json`)

`antipages.json` is the exclusive source of variation. It is pure data, never presentation.

### Required Fields
* `slug`
* `service`
* `jurisdiction`
* `variant`
* `audience`
* `seo` (optional object)

If present, `seo` may only contain:
- title
- description
- canonical

No additional fields allowed.

### Prohibitions
The data layer stringently prohibits the inclusion of:
* HTML tags
* CSS classes
* Visual flags
* Dynamic blocks
* Structural conditionals
* Rich content execution logic

JSON = pure data. Never presentation.

---

## 3. Template Structural Blocks (Mandatory Order)

The AntiPage interface consists of a fixed, immutable order of blocks. Modification, omission, or substitution is forbidden.

1. **Hero**: Contains the parametrically generated H1 and the core value proposition. Cannot contain dynamic marketing banners.
2. **Context**: Defines the geographical and service-specific baseline. Cannot contain emotional storytelling.
3. **Execution Scope**: Explicitly defines what the service does and delivers. Cannot contain edge-case disclaimers as separate micro-sections.
4. **Irreversibility Statement**: Explains the immutable and non-refundable nature of the event. Cannot contain mitigating promotional language.
5. **Process Summary**: Outlines the progression strictly at the Landing-level, independent of backend Engine states. Cannot display live state or trackers.
6. **Trust / Structural Guarantees**: Confirms legal or structural verifiability. Cannot contain conditional testimonials or exclusive FAQs.
7. **Related Procedures (Internal Crawl Graph)**: Programmatically dynamic block bridging the siloed service architecture. Extracts up to 4 disparate procedures identically bound by `jurisdiction`. Enforces graph entropy via randomization. Eliminates non-crawlable singletons.
8. **CTA Block**: Contains the single interaction element routing to the Engine. Cannot contain alternative links.

**Prohibitions:**
* Ad hoc micro-sections are prohibited.
* Reordering of blocks is prohibited.

Internal conditional rendering inside blocks is prohibited.

Blocks may receive parametric text, but may not:
- Hide sub-sections per variant
- Inject exclusive components
- Change internal hierarchy

### Legal Layout Footer (Global — Outside Template)

A minimal `<footer>` element is rendered **after** the CTA block, as a global layout element of the `AntiPage` component. It is **not a template block** and does not alter the block order, count, or invariant.

**Content (fixed, non-parametric):**
- Link: `Términos de Servicio` → `/legal/terms`
- Link: `Política de Privacidad` → `/legal/privacy`
- Text: `Cyboring Technologies LLC`

**Visual constraints:** `text-xs`, `text-muted-foreground`, centered, separated from CTA by a `border-t`.

**Prohibitions for this footer:**
- Must not contain additional navigation links
- Must not contain marketing copy
- Must not contain icons
- Must remain static (no SSR, no fetch, no runtime logic)
- Must not be moved inside any template block

---

## 4. H1 Pattern Contract

The H1 employs a mandatory structural formula.

### Structural Example
`H1 = {service_label} + " in " + {jurisdiction_label}`

The H1 must be programmatically derived from the JSON data layer. Manual overrides are prohibited.

### Prohibitions
* Creative H1s
* Emotional H1s
* H1 variables dynamically modified per variant
* Multiplicity of H1s per page

---

## 5. Variant Semantics (V1–V4)

The AntiPage taxonomy governs semantics only. The variant defines the specific angle of the content injected into the invariant blocks.

* **V1**: Direct transactional framing.
* **V2**: Problem-mapped framing.
* **V3**: B2B semantic emphasis.
* **V4**: B2C semantic emphasis.

### Invariants per Variant
* No layout change.
* No block change.
* No visual change.
* Only micro-semantics within the same block change.

---

## 6. CTA Invariant

Execution is routed exclusively to the Engine. The Call to Action complies with the following invariants:

* A single primary CTA exists on the page.
* Copy must be neutral.
* Execution opens directly.
* No intermediate steps.
* No lead capture.
* No external forms.
* No dynamic pricing widget.

The legal layout footer (see Section 3) is rendered **after** the CTA and is not considered an additional CTA or navigation element. The CTA invariant remains unviolated.

This is subordinate to `README_LANDING.md`.

---

## 7. SEO Governance

Search Engine Optimization metrics follow a rigid, reproducible formula to ensure statistical comparability between pages.

* **Title Tag Pattern**: `[Service] en [Jurisdiction] — Escrito legal listo para presentar | documentos.legal`
* **Meta Description Pattern**: `Genere su documento legal para [servicio] en [jurisdicción]. Listo para presentar en minutos. Sin cuentas. Sin almacenamiento.`
* **Structured Data Rule**: Each AntiPage must inject a parametric `Service` JSON-LD schema (mapping `provider`, `brand`, `areaServed`, `url`) and a `BreadcrumbList` schema reflecting the canonical path.
* **Canonical Rule**: Base canonical mapped purely to the route matrix.
* **Manifest Injection Rule**: To eradicate indexation latency, a flat programmatic index of canonical URLs must be regenerated at `seo/indexation_manifest.json` enabling Search Console API bulk submissions.
* **Prohibitions**: No keyword stuffing, no mandatory blog interlinking, no sidebar.

Statistical comparability between pages is confirmed by these rules.

---

## 8. Expansion Rules

The taxonomy expands only via strictly defined additions to the JSON configuration:

* **How to add new jurisdictions**: Expansion occurs exclusively through structured additions to `antipages.json`, in strict compliance with ANTI_PAGES_MASTER_INVENTORY_V1.md.

  No structural deviation from the 96-page matrix is allowed without issuing version 2 of this contract.
* **How to add new services**: Add root service configurations in the data layer.
* **How to add new variants**: Introduce new semantic parameters bound to existing constraints.
* Any structural change requires version 2 of the contract.

---

## 9. Absolute Prohibitions

Explicit list of absolute prohibitions:

* Multiple layouts
* Subcomponents per service
* Duplicate templates
* Banners per variant
* Exclusive FAQs per page
* Conditional testimonials
* Dynamic pricing
* Customization
* Visual flags
* Persistence

---

## 10. Final Structural Invariant

This contract guarantees total industry uniformity. By locking layout and isolating content in the pure data layer, SBU-Legal guarantees strict mathematical comparability of performance across all instances.

The model ensures precise, immediate, and annual reproducibility of the complete scope (96 pages). Everything defined herein is unyieldingly subordinate to the One-Shot model.
