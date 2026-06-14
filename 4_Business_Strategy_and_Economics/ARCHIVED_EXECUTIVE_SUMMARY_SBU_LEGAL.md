---
id: "ARCHIVED_EXECUTIVE_SUMMARY_SBU_LEGAL"
title: "Archived Executive Summary — SBU-Legal"
type: "Business Strategy, Marketing & Economics"
version: "v4.0"
last_updated: "2026-06-14"
status: "Archived / KILL Executed"
---

# Archived Executive Summary — SBU-Legal

**Effective date:** June 14, 2026  
**Business unit:** SBU-Legal  
**Public domain:** [documentos.legal](https://documentos.legal)  
**Institutional owner:** [Cyboring Technologies LLC](https://cyboring.com)  
**Decision:** KILL / Archive  
**Decision confidence:** High

This document is the current executive summary for SBU-Legal. It replaces the former operational
summary and must not be interpreted as a commercial plan, active product specification, revenue
forecast, or authorization to reactivate the service.

---

## 0. Executive Status

| Dimension | Current State |
|---|---|
| Business status | Archived; no active commercial operation |
| Public website | Institutional archive only |
| Public purchases | Disabled |
| File uploads and processing | Disabled |
| Document generation and delivery | Disabled |
| Engine hostname | Restricted; returns `410 Gone` |
| Payment gateway hostname | Restricted; returns `410 Gone` |
| SEO posture | Only the archived root page is indexable |
| Current investment priority | None |
| Reusable technical assets | Preserved internally |

SBU-Legal is no longer an operating business unit. Documentos.legal remains online solely as an
institutional record and as a controlled holder for the domain and brand.

---

## 1. Decision Summary

The former product attempted to sell automated procedural legal documents through a one-shot,
pay-per-use workflow. The infrastructure demonstrated useful technical capabilities, but the
commercial thesis did not justify continued investment.

The decisive issues were:

1. No auditable evidence of repeatable demand, conversion, CAC, revenue, or dispute performance.
2. High legal and reputational risk from probabilistic outputs in a category governed by accuracy,
   traceability, jurisdictional maintenance, and professional responsibility.
3. Public claims that exceeded the verifiable capabilities and safeguards of the runtime.
4. A privacy-first differentiator that did not solve the buyer's dominant concern: legal trust.
5. Higher expected return from allocating founder attention to other SBUs.

The approved action was to archive the business, remove the public commercial surface, preserve
selected infrastructure, and prohibit implicit reactivation.

---

## 2. What SBU-Legal Was

SBU-Legal was an experimental legal-document automation initiative operated under the
Documentos.legal brand.

Its former design included:

- A transactional, pay-per-use document workflow.
- PDF/DOCX ingestion, extraction, preview, transformation, and delivery.
- A payment gateway using signed quotes and payment-intent orchestration.
- Ephemeral storage and session-destruction patterns.
- A static marketing site with localized commercial pages, programmatic SEO pages, and blog
  content.

These descriptions are historical. They do not represent currently available services.

---

## 3. What It Is Not

Documentos.legal is not:

- An active legal-document generation service.
- A law firm or legal-services provider.
- A source of legal advice or representation.
- A public upload, processing, purchase, or download workflow.
- A supported SaaS product.
- A business currently seeking traffic, conversion, revenue, or customer retention.

No historical material should be used as a substitute for qualified professional advice.

---

## 4. Production Archive State

The KILL decision was executed in production on June 14, 2026.

### Public Landing

- `https://documentos.legal` returns an institutional archive page.
- The page clearly states that Documentos.legal is archived.
- The only external institutional link is a discreet link to
  [Cyboring Technologies LLC](https://cyboring.com).
- Commercial CTAs, forms, upload controls, checkout paths, service pages, pricing, FAQ, blog, and
  programmatic SEO pages were removed.
- Legacy localized and operational landing routes redirect to `/`.

### Engine

- `https://engine.documentos.legal` is restricted by a reversible archive kill-switch.
- All tested routes return `410 Gone`.
- Responses include `no-store` and `noindex, nofollow, noarchive`.
- Operational code and Durable Object contracts remain preserved internally.

### Gateway

- `https://gateway.documentos.legal` is restricted by a reversible archive kill-switch.
- Quote, payment-intent, webhook, and other tested routes return `410 Gone`.
- Responses include `no-store` and `noindex, nofollow, noarchive`.

### Active Production References

| Surface | Active Reference |
|---|---|
| Landing source commit | `5b9caf6` |
| Cloudflare Pages deployment | `cabd1cd6-2bc8-4222-9318-658154a02d9b` |
| Engine archive Worker version | `3c00d344-75df-41c2-86ab-a1e06a3efdc5` |
| Gateway archive Worker version | `c0927c03-7caa-4767-9f11-2da92c740ad0` |
| Engine kill-switch source commit | `a547623` |
| Gateway kill-switch source commit | `ddcbbc0` |

---

## 5. SEO and Public Content State

- The sitemap contains only `https://documentos.legal`.
- The root archive page is the only approved indexable page.
- Legacy locale, engine, prepare, terminal, sitemap, and API paths are disallowed in robots rules.
- Service, offer, FAQ, navigation, and transactional structured data were removed.
- The RSS feed is a neutral archive feed with no promotional entries.
- AntiPages, localized commercial routes, weak blog content, promotional assets, and public sample
  downloads were removed.
- Final public export and public-source searches returned zero matches for the identified sensitive
  commercial and unsupported-claim terms.

---

## 6. Financial and Commercial State

Former pricing, MRR forecasts, conversion targets, CAC targets, SEO projections, gross-margin
scenarios, and growth plans are historical hypotheses only.

They are not:

- Actual performance.
- Approved budgets.
- Current operating targets.
- Evidence of monetization.
- A basis for reopening the SBU.

The current approved financial posture is:

- No acquisition spend.
- No product-development allocation.
- No revenue target.
- No customer-support obligation.
- Minimize passive infrastructure cost while preserving reusable assets.

---

## 7. Assets Preserved

The following assets remain available for internal reuse:

- The `documentos.legal` domain and brand.
- Engine and gateway repositories.
- PDF/DOCX ingestion, extraction, preview, and transformation patterns.
- Ephemeral-storage and session-destruction patterns.
- R2, Durable Object, signed-quote, and payment-orchestration learnings.
- Reusable UI, deployment, and infrastructure components.
- Historical architecture, economics, and product-learning documentation.

Preservation does not imply public availability, support, continuity, or authorization to deploy
the former operational configurations.

---

## 8. Assets and Theses Retired

The following are retired as active business strategy:

- Generic procedural documents marketed as ready for legal use.
- Programmatic legal-service AntiPages.
- Jurisdiction expansion without verified legal datasets and accountable review.
- One-shot irreversibility as a primary legal-product value proposition.
- Unsupported claims of legal-grade accuracy, guaranteed outcomes, or runtime capabilities.
- Revenue projections presented without observed commercial evidence.
- A zero-human-support assumption for high-risk legal outputs.

---

## 9. Governance and Operational Controls

### Mandatory Archive Controls

1. Production engine deployments must use `wrangler.archive.toml`.
2. Production gateway deployments must use `wrangler.archive.toml`.
3. The standard operational Wrangler configurations must not be deployed while the KILL decision
   remains active.
4. The landing must not link to the engine, gateway, checkout, upload, generation, or download
   flows.
5. The root archive page must remain the only indexable public page.
6. Historical documents must retain clear archived context and must not be represented as current
   strategy.

### Reactivation Risk

A future deployment using the normal engine or gateway configuration could technically reactivate
services. Repository access and deployment procedures must therefore treat the archive
configurations as the approved production state.

---

## 10. Reopening Criteria

SBU-Legal may only be reconsidered as a new, narrowly scoped thesis. Reopening requires all of the
following:

1. A new written executive decision explicitly reversing KILL status.
2. One defined professional buyer, one legal act, and one jurisdiction.
3. Verified willingness to pay before material rebuilding.
4. A maintained and traceable legal source base.
5. Objective output evaluation by qualified professionals.
6. Coherent claims, terms, privacy controls, support, recovery, and dispute handling.
7. Auditable acquisition and unit-economics evidence.
8. A new legal and reputational risk review.

Preserved code, domain ownership, demos, impressions, compliments, or free users do not qualify as
reactivation signals.

---

## 11. Final Executive Decision

**SBU-Legal remains ARCHIVED / KILL.**

Do not invest additional founder time, acquisition budget, legal-content production, or product
development into the former thesis. Preserve selected technical assets and institutional learning.
Any future legal-product opportunity must begin as a new validation effort and must not inherit an
assumption of continuity from Documentos.legal.

---

## 12. Related Records

- `ARCHIVE_DECISION_2026-06-14.md` — normative archive decision and production execution record.
- `VEREDICTO_EJECUTIVO_SBU_LEGAL_2026-06-14.md` — audit findings and rationale for KILL.
- `ARCHIVED_EXECUTIVE_SUMMARY_V3.3_SBU_LEGAL.md` — historical pre-archive executive summary.
- `EXECUTIVE_SUMMARY_V3.3_SBU_LEGAL.md` — former operational summary, retained only if explicitly
  marked as historical.

