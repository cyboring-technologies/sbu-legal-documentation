---
id: "CLOUDFLARE_DEPLOYMENT_ARCHITECTURE"
title: "Cloudflare Deployment Architecture"
type: "Core Architecture and Systems"
version: "v1.0"
last_updated: "2026-03-10"
status: "Approved"
---

# Cloudflare Deployment Architecture

**Context:** *This document details the serverless Cloudflare infrastructure, domain topology, and component deployment boundaries used by SBU-Legal.*

---

# 1. Purpose

This document defines the **Cloudflare infrastructure architecture** used to deploy and operate the SBU‑Legal system.

It specifies:

- Domain routing
- Cloudflare services used
- Worker topology
- Durable Object namespaces
- Environment variables scope
- Deployment boundaries between components

This document **does not redefine application architecture**.  
Application logic is governed by:

- `README_ENGINE_V2.md`
- `README_GATEWAY_V2.md`
- `BASE_EXECUTION_CONTRACT.md`

This document strictly describes **infrastructure deployment**.

---

# 2. Cloudflare Services Used

The system uses the following Cloudflare components:

| Component | Purpose |
|---|---|
Cloudflare Pages | Static hosting for the Landing website |
Cloudflare Workers | Runtime for Gateway and Engine |
Durable Objects | Stateful execution environment for Engine sessions |
Cloudflare DNS | Domain routing |
Cloudflare CDN | Global edge distribution |
Cloudflare TLS | HTTPS termination |

The system is **fully serverless**.

No traditional server infrastructure exists.

---

# 3. Domain Topology

Primary domain:

```
documentos.legal
```

Infrastructure routing:

| Domain | Component |
|---|---|
documentos.legal | Landing Page (Cloudflare Pages) |
engine.documentos.legal | Engine Worker |
gateway.documentos.legal | Gateway Worker |

Example routing:

```
https://documentos.legal
→ Marketing Landing
```

```
https://engine.documentos.legal
→ Sovereign Engine runtime
```

```
https://gateway.documentos.legal
→ Payment authority validation
```

---

# 4. Component Architecture

System components deployed to Cloudflare:

```
Landing (Pages)
Engine (Worker + Durable Object)
Gateway (Worker)
```

Logical structure:

```
User
  |
  v
Landing Page (Cloudflare Pages)
  |
  v
Engine Worker
  |
  v
Gateway Worker
  |
  v
Stripe Payment API
```

---

# 5. Landing Deployment

Landing repository:

```
sbu-legal-landing
```

Deployment target:

```
Cloudflare Pages
```

Build process:

```
next build
next export
```

Output directory:

```
/out
```

Pages configuration:

```
Framework: Next.js (static export)
Build command: npm run build
Output directory: out
```

Landing responsibilities:

- Marketing content
- SEO surface
- Blog content
- Legal pages
- CTA entry point to Engine

Landing has **no authority over execution or payment**.

---

# 6. Engine Deployment

Engine repository:

```
sbu-legal-engine
```

Deployment target:

```
Cloudflare Worker
```

Worker responsibilities:

- Document ingestion
- Parsing
- Prompt generation
- LLM execution
- Draft generation
- Validation
- Artifact generation
- Session incineration

*Update (2026-03-10): Engine Worker infrastructure finalized with `wrangler.toml` and successfully deployed to production. Domain `engine.documentos.legal` is correctly attached to the fetch handler.*

---

# 7. Durable Objects

The Engine uses **Durable Objects** to maintain execution runtime.

Each session creates a single instance.

Properties:

```
1 Engine per session
1 runtime per session
RAM‑only state
No persistence
```

Durable Object namespace example:

```
ENGINE_SESSION_OBJECT
```

Lifecycle:

```
Create → Execute → Destroy
```

Termination events:

- Download complete
- Execution failure
- Session abandonment

After termination:

```
All memory destroyed
```

This enforces the **Incineration Invariant**.

---

# 8. Gateway Deployment

Gateway repository:

```
sbu-legal-gateway
```

Deployment target:

```
Cloudflare Worker
```

Gateway responsibilities:

- Stripe payment validation
- Execution token issuance
- Rubicon enforcement

Gateway **never hosts UI**.

Gateway is invoked only during the payment event.

Reference architecture:

See `README_GATEWAY_V2.md`.

*Update (2026-03-10): Infrastructure finalized with `wrangler.toml` and verified through production deployment to `gateway.documentos.legal`. Confirmed environmental bindings for `STRIPE_SECRET_KEY` and `STRIPE_WEBHOOK_SECRET`.*
*Update (2026-03-11): Confirmed DNS routing requires manual `CNAME` pointing to `<account-subdomain>.workers.dev` via Cloudflare Dashboard to resolve. Wrangler `routes` is used for pattern matching internal to Cloudflare but does not auto-provision DNS for Gateway.*

---

# 9. Worker Routes

Workers are attached using Cloudflare routes.

**CRITICAL NOTE FOR GATEWAY:** The Gateway requires a manual `CNAME` record in the Cloudflare Dashboard pointing `gateway` to the `sbu-legal-gateway.<account-subdomain>.workers.dev` target with Proxy (Orange Cloud) enabled to resolve globally.

Example:

```
engine.documentos.legal/*
→ Engine Worker
```

```
→ Gateway Worker

*Update (2026-03-10): All worker routes confirmed active. Engine Worker correctly responds at `engine.documentos.legal/*` after successful production push.*
```

Workers operate entirely at the edge.

---

# 10. Environment Variables

Environment variables are configured in:

```
Cloudflare Worker Settings
```

Variables include:

```
STRIPE_ENV_MODE
STRIPE_SECRET_KEY_LIVE
STRIPE_WEBHOOK_SECRET_LIVE
LLM_PRIMARY_API_KEY
LLM_FALLBACK_API_KEY
```

Variables **must never be committed to the repository**.

Detailed registry is defined in:

```
ENVIRONMENT_VARIABLES_REGISTRY.md
```

---

# 11. Security Model

Security layers:

1. HTTPS enforced globally
2. Cloudflare WAF protections
3. No persistent storage
4. Stripe tokenized payment processing
5. Stateless Gateway design

Session data **never persists** beyond runtime memory.

---

# 12. Observability

Because sessions are incinerated:

The system stores **no execution logs** internally.

Operational monitoring must occur via:

- Stripe dashboard
- Cloudflare analytics
- Manual transaction counters

The architecture deliberately avoids internal persistence.

---

# 13. Deployment Workflow

Deployment occurs independently per component. There is **no global CI/CD pipeline** (like GitHub Actions) configured for the backend workers by design.

Landing:

```
Git push → Cloudflare Pages auto-deploy
```
*(Cloudflare natively intercepts the GitHub push to deploy the static site.)*

Workers (Engine & Gateway):

```
wrangler deploy
```
*(Workers MUST be pushed manually from the local development machine using the Wrangler CLI. A `git push` to GitHub will NOT update the production Cloudflare Workers.)*

Typical sequence:

```
1 Deploy Engine Worker (`npx wrangler deploy`)
2 Deploy Gateway Worker (`npx wrangler deploy`)
3 Deploy Landing Pages (`git push`)
```

---

# 14. Failure Model

Possible failure classes:

| Failure | Handling |
|---|---|
LLM timeout | Execution fails → incineration |
Validator failure | Session destroyed |
Stripe failure | Payment canceled |
Worker crash | Session destroyed |

No retries occur after the Rubicon.

---

# 15. Architectural Guarantees

The Cloudflare architecture ensures:

- Global edge execution
- Minimal latency
- Stateless infrastructure
- Automatic scaling
- No server maintenance

All execution environments are ephemeral.

---

# 16. Final Principle

Infrastructure exists only to enable **one execution**.

After completion:

```
Session destroyed
Authority consumed
Engine dismantled
```

Nothing remains.

# 17. LLM Execution Time Constraints

Cloudflare Workers operate under strict request lifecycle and CPU time limits.

Because SBU-Legal performs LLM document generation during execution, generation must complete within the Worker request lifecycle.

If an upstream LLM call exceeds runtime limits:

- the Worker request may terminate
- the Engine session is destroyed
- the session is incinerated
- the PaymentIntent is canceled

The Engine must enforce strict upstream timeouts when calling LLM providers.

This prevents sessions from entering undefined states after the Rubicon.

# 18. Durable Object Runtime Assumptions

Durable Objects provide per-session execution environments but are not guaranteed to remain resident indefinitely.

Cloudflare may perform:

- instance eviction
- cold restarts
- instance migration

The Engine must therefore assume:

- no long-term memory guarantee
- no persistence across runtime restarts
- possible cold starts during execution

All Engine state must remain fully reconstructable from in-memory session context during the active execution window.

This design assumption aligns with the Incineration Invariant and the absence of persistent storage.
