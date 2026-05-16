# Offsetta

**Programmable mobile money ↔ blockchain financial rails, built on Stellar.**

Africa moves money on mobile and the new world settles transactions on-chain. Offsetta is the infrastructure layer that connects both by giving developers a single API to build products that span mobile money networks, stablecoins, and cross-border payments, without rebuilding the plumbing every time.

> Built for Africa. Open to the world.

---

## You might be asking "Why Offsetta?"

Mobile money has transformed financial access across Africa — but it remains largely isolated from the broader global financial system. Moving value between M-Pesa, a USDC wallet, a Nigerian bank account, or a Kenyan fintech still requires bespoke integrations, fragmented liquidity, and slow settlement.

Offsetta solves this by providing a unified, programmable settlement layer:

- **For developers** — one REST API to onramp, offramp, and route value across networks
- **For fintechs** — plug into existing corridors without negotiating liquidity independently
- **For the ecosystem** — open, composable infrastructure that anyone can build on or contribute to

---

## What It Does

| Layer | What it handles |
|---|---|
| **Fiat Onramp** | Accept mobile money (such as M-Pesa, MTN MoMo, Airtel) and mint on-chain stablecoins |
| **Offramp** | Redeem stablecoins back to mobile money or bank accounts |
| **Routing Engine** | Intelligent path-finding across corridors and liquidity sources |
| **Liquidity Layer** | Pooled on-chain liquidity for instant, deterministic settlement |
| **Developer API** | REST + webhook API for fintechs and wallets to integrate against |

---

## Architecture

Offsetta is structured as a three-layer stack:

```
┌─────────────────────────────────────────────────────────┐
│                     apps/web (Next.js)                  │
│              Dashboard · Docs · Status Page             │
└────────────────────────┬────────────────────────────────┘
                         │ REST / WebSocket
┌────────────────────────▼────────────────────────────────┐
│                    apps/api (Node.js)                   │
│         Onramp · Offramp · Routing · Webhooks           │
└────────────────────────┬────────────────────────────────┘
                         │ Stellar SDK / Soroban RPC
┌────────────────────────▼────────────────────────────────┐
│              contracts/ (Soroban / Rust)                │
│  CustodyLedger · SettlementEscrow · LiquidityPool       │
│  FeeEngine · ComplianceRegistry                         │
└─────────────────────────────────────────────────────────┘
```

The API layer handles business logic, provider integrations, and webhook delivery. The smart contract layer — built on Stellar's Soroban — handles custody, settlement finality, liquidity, and compliance hooks on-chain.

---

## Proposed Monorepo Structure

```
offsetta/
├── apps/
│   ├── web/          # Next.js dashboard & developer portal
│   └── api/          # Node.js REST API & webhook engine
├── contracts/
│   ├── custody-ledger/
│   ├── settlement-escrow/
│   ├── liquidity-pool/
│   ├── fee-engine/
│   └── compliance-registry/
├── packages/
│   └── sdk/          # Shared TypeScript SDK (API client + Stellar helpers)
├── docs/
│   ├── architecture.md
│   ├── api-reference.md
│   └── contracts.md
└── README.md
```

---

## Tech Stack

| Area | Technology |
|---|---|
| Blockchain | Stellar · Soroban (Rust) |
| Stablecoin | USDC (Circle) |
| Backend | Node.js · Express · TypeScript |
| Frontend | Next.js · Tailwind CSS |
| Database | PostgreSQL · Redis |
| Infra | Docker · GitHub Actions |

---

## Getting Started

### Prerequisites

- Node.js ≥ 20
- Rust + `soroban-cli`
- Docker (for local Postgres + Redis)

### Install

```bash
git clone https://github.com/your-org/offsetta.git
cd offsetta
npm install
```

### Run locally

```bash
# Start the API
cd apps/api && npm run dev

# Start the web dashboard
cd apps/web && npm run dev
```

### Build contracts

```bash
cd contracts/settlement-escrow
cargo build --target wasm32-unknown-unknown --release
```

Full local environment setup, environment variables, and testnet configuration are documented in [`docs/architecture.md`](./docs/architecture.md).

---

## MVP Scope

The current focus is a lean, working core:

- [ ] USDC onramp via mobile money (one corridor)
- [ ] USDC offramp to mobile money
- [ ] REST API with API key auth
- [ ] Settlement Escrow contract (Soroban)
- [ ] Liquidity Pool contract (Soroban)


---

## Contributing

Offsetta is fully open source and community-driven. **This is a good time to get involved** — the core architecture is defined, the contracts are scoped, and there is meaningful, concrete work across every part of the stack.

Whether you write Rust, TypeScript, or just have strong opinions about payment UX, there is a place for you here.

### Where to start

1. **Browse open issues** — look for `good first issue` or `help wanted` labels
2. **Fork and branch** — `git checkout -b feat/your-feature`
3. **Build and test** — make your changes and add tests where relevant
4. **Open a PR** — include a clear description of what changed and why
5. **Review** — a maintainer will review within 3–5 business days

### Open contribution areas

| Area | What's needed |
|---|---|
| **Smart contracts** | Rust, Soroban SDK — core settlement and liquidity logic |
| **API** | TypeScript, Node.js — onramp/offramp flows, webhook engine |
| **Frontend** | React, Next.js, Tailwind — developer portal and dashboard |
| **Mobile money integrations** | API integration, fintech domain knowledge |
| **Docs & DX** | Technical writing — setup guides, API reference, tutorials |
| **Security** | Auditing, threat modelling — especially contract layer |

### Guidelines

- Follow existing code style: ESLint + Prettier for TypeScript, `rustfmt` for Rust
- Keep PRs focused — one feature or fix per PR
- Write meaningful commit messages using conventional prefixes: `feat:`, `fix:`, `docs:`, `chore:`
- All smart contract changes require a written rationale in the PR description
- Be respectful — see [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)

### Reporting bugs

Open an issue with the `bug` label. Include steps to reproduce, expected vs. actual behaviour, and your environment details.

### Security vulnerabilities

Do **not** open a public issue. Email **security@offsetta.xyz** directly.

---

## Roadmap

| Phase | Focus |
|---|---|
| **Phase 1 — MVP** | USDC rail · one corridor · core API |
| **Phase 2** | Multi-corridor · liquidity pools · TypeScript SDK |
| **Phase 3** | Compliance registry · KYC hooks · partner integrations |
| **Phase 4** | Decentralised routing · protocol governance |

---

## License

[MIT](./LICENSE)
