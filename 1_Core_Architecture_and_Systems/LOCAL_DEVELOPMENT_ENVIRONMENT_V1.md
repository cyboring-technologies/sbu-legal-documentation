---
id: "LOCAL_DEVELOPMENT_ENVIRONMENT_V1"
title: "Local Development Environment & Setup"
type: "Core Architecture and Systems"
version: "v1.0"
last_updated: "2026-03-18"
status: "Approved"
---

# Local Development Environment & Setup

**Context:** *Operational guide for initializing and running the SBU-Legal services locally for development and testing, ensuring port alignment and configuration consistency.*

---

## 1. System Topology (Local)

To simulate the Cloudflare serverless environment locally, the system is split into four distinct services that must run simultaneously.

| Component | Directory | Local URL | Runtime |
| :--- | :--- | :--- | :--- |
| **Landing** | `sbu-legal-landing` | `http://localhost:3000` | Next.js (Node) |
| **Gateway** | `sbu-legal-gateway` | `http://localhost:8787` | Node.js (Server Wrapper) |
| **Engine** | `sbu-legal-engine` | `http://localhost:8788` | Wrangler (Miniflare) |
| **Stripe CLI** | Project Root | `localhost:8787/webhook` | Binary (Go/Stripe) |

---

## 2. Configuration Strategy

Local development utilizes file-based configuration to ensure isolation and prevent accidental use of production keys.

### 2.1. Environment Files
- **Landing**: Uses `.env.local` for Next.js environment variables.
- **Engine**: Uses `.dev.vars` (parsed by Wrangler) for secrets and `wrangler.toml` for public vars.
- **Gateway**: Uses `.dev.vars` (parsed by `server.mjs`) for secrets and `wrangler.toml` for public vars.

### 2.2. Stripe Immutability
The system enforces a strict `STRIPE_ENV_MODE="test"` invariant in local development.
- All keys in `.dev.vars` must have the `_TEST` suffix (e.g., `STRIPE_SECRET_KEY_TEST`).
- The presence of `_LIVE` keys in a `test` environment will trigger a fatal crash before initialization.

---

## 3. Startup Procedures

Open four separate terminal instances to start the full environment.

### Step 1: Stripe Webhook Listener
The Stripe CLI must be authenticated and configured to forward webhooks to the Gateway.
```powershell
# Authenticate (One-time or after 90 days)
./stripe.exe login

# Start Listener
./stripe.exe listen --forward-to localhost:8787/webhook
```

### Step 2: Marketing Landing
Starts the Next.js development server.
```powershell
cd sbu-legal-landing
npm run dev
```

### Step 3: Business Logic (Engine)
Starts the Miniflare environment for the Cloudflare Worker. Port 8788 is enforced via `wrangler.toml`.
```powershell
cd sbu-legal-engine
npm run dev
```

### Step 4: Security Gateway
Starts the Node.js development wrapper that loads the Worker logic. Port 8787 is enforced via `server.mjs`.
```powershell
cd sbu-legal-gateway
node server.mjs
```

---

## 4. Operational Invariants

1.  **Gateway Entry Point**: All Stripe webhooks **must** target the Gateway (Port 8787). The Gateway performs signature verification before internal propagation.
2.  **Engine Isolation**: The Engine (Port 8788) should not be accessed directly by the Stripe CLI or the public unless proxied.
3.  **Key Consistency**: `SESSION_SECRET` must be identical across all `.dev.vars` files to ensure JWT tokens issued by the Gateway are accepted by the Engine.
4.  **Local Binary**: The `stripe.exe` binary should be maintained in the project root for consistent access without requiring global PATH modifications.
