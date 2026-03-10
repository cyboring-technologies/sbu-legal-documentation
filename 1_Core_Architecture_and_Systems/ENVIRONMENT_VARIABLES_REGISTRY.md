---
id: "ENVIRONMENT_VARIABLES_REGISTRY"
title: "Environment Variables Registry"
type: "Core Architecture and Systems"
version: "v1.0"
last_updated: "2026-03-09"
status: "Approved"
---

# Environment Variables Registry

**Context:** *This document centralizes the configuration registry of environment variables required for production and development deployments within the Cloudflare ecosystem.*

---

# 1. Purpose

This document defines the **complete registry of environment variables** required to operate the SBU‑Legal system in production and development environments.

It exists to:

- Centralize configuration
- Prevent deployment errors
- Define variable scope per component
- Ensure secure key management

No secret values should ever be committed to the repository.

Only **variable names and descriptions** appear in this document.

---

# 2. Scope

Environment variables are used in the following runtime components:

| Component | Runtime |
|---|---|
Landing | Cloudflare Pages |
Engine | Cloudflare Worker |
Gateway | Cloudflare Worker |

Variables are configured through:

```
Cloudflare Dashboard
or
Wrangler secrets
```

---

# 3. Security Rule

Secrets **must never appear in:**

- Git repositories
- CI logs
- Client-side code
- Public documentation

All secrets must be injected through:

```
wrangler secret put VARIABLE_NAME
```

or Cloudflare dashboard settings.

---

# 4. Stripe Configuration

Used by **Gateway Worker** and **Engine Worker**.

| Variable | Description |
|---|---|
STRIPE_SECRET_KEY | Stripe secret API key used to create and capture PaymentIntents |
STRIPE_PUBLISHABLE_KEY | Public Stripe key used by the frontend payment form |
STRIPE_WEBHOOK_SECRET | Secret used to validate Stripe webhook signatures |

Example environment scope:

```
Gateway Worker
Engine Worker
```

---

# 5. LLM Provider Configuration

Used by **Engine Worker**.

| Variable | Description |
|---|---|
LLM_PRIMARY_API_KEY | API key for the primary LLM provider |
LLM_FALLBACK_API_KEY | API key for fallback LLM provider |

These keys authorize calls to the legal generation engine.

---

# 6. Service Endpoint Configuration

Used for internal service routing.

| Variable | Description |
|---|---|
ENGINE_ORIGIN | Base URL of the Engine Worker |
GATEWAY_ORIGIN | Base URL of the Gateway Worker |
LANDING_ORIGIN | Base URL of the Landing site |

Example values:

```
ENGINE_ORIGIN=https://engine.documentos.legal
GATEWAY_ORIGIN=https://gateway.documentos.legal
LANDING_ORIGIN=https://documentos.legal
```

---

# 7. Durable Object Configuration

Used by **Engine Worker**.

| Variable | Description |
|---|---|
ENGINE_DO_NAMESPACE | Durable Object namespace identifier for engine sessions |

This namespace binds the session runtime to a unique Durable Object instance.

---

# 8. Feature Flags (Optional)

Feature flags allow controlled activation of experimental features.

| Variable | Description |
|---|---|
ENGINE_DEBUG_MODE | Enables diagnostic logging in development |
VALIDATOR_STRICT_MODE | Enables stricter output validation checks |

These flags should remain disabled in production.

---

# 9. Environment Profiles

Typical environments:

```
development
staging
production
```

Production must use:

- Stripe Live keys
- Production LLM keys
- Production domain origins

---

# 10. Worker Configuration Example

Example configuration using Wrangler:

```
wrangler secret put STRIPE_SECRET_KEY
wrangler secret put STRIPE_WEBHOOK_SECRET
wrangler secret put LLM_PRIMARY_API_KEY
wrangler secret put LLM_FALLBACK_API_KEY
```

Non-secret variables may appear in:

```
wrangler.toml
```

Example:

```
[vars]
ENGINE_ORIGIN="https://engine.documentos.legal"
GATEWAY_ORIGIN="https://gateway.documentos.legal"
LANDING_ORIGIN="https://documentos.legal"
```

---

# 11. Rotation Policy

Secrets should be rotated under the following conditions:

- Credential leak suspected
- Provider request
- Annual security rotation

Rotation procedure:

1. Generate new key in provider dashboard
2. Update Cloudflare secret
3. Redeploy worker

---

# 12. Failure Modes

Misconfigured environment variables can produce:

| Failure | Cause |
|---|---|
Stripe payment failure | Missing Stripe secret |
LLM execution failure | Invalid API key |
Worker crash | Missing required variable |
Routing failure | Incorrect origin URL |

All deployments must verify environment variables before production release.

---

# 13. Operational Checklist

Before deploying to production verify:

```
Stripe keys configured
LLM keys configured
Worker origins correct
Durable Object namespace bound
Secrets injected via Wrangler
```

---

# 14. Final Rule

Environment variables define **runtime authority over external systems**.

Incorrect configuration can break:

- payment processing
- document generation
- execution flow

All variables must be verified before deployment.

