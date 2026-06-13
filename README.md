# Secant Pay

Secant Pay is a self-custodial crypto payments platform for merchants accepting stablecoin payments on Base and Solana.

Merchants connect their own wallets, create payment requests, optionally send the request to a customer's Solana wallet inbox, and receive funds directly to addresses they control. Secant never holds private keys or custodies funds. The platform tracks payment state around on-chain transfers and provides the merchant tooling layer: checkout, invoices, point-of-sale, payment links, Blinks, notifications, portfolio visibility, swap routing, and settlement detection.

## Why Secant

**Non-custodial by design.** Every payment settles directly from customer wallet to merchant wallet. Secant observes and verifies — it does not intermediate.

**Two chains, one interface.** Base for EVM USDC payments with Zerion-powered portfolio and routing. Solana for Solana Pay, Jupiter-powered SPL checkout, Secant Blinks, SNS names, Dialect payment request alerts, and native settlement detection via Helius webhooks.

**Merchant-first.** Built for freelancers, agencies, global merchants, and Solana-native teams who need checkout, invoicing, customer payment requests, and settlement tracking without giving up custody.

## Current State

Phase 1 is live with multi-wallet dashboard, terminal checkout, Scan & Pay point-of-sale, invoice generation with pay links, wallet QR, Secant Blinks, optional Dialect customer requests, swap and bridge routing, and Helius webhook settlement on Solana. See [Phase 1: Current Build](./phase-1-current-build.md) for the full feature set.

## Roadmap

| Phase | Focus | Status |
|-------|-------|--------|
| [Phase 1](./phase-1-current-build.md) | Core checkout, invoices, payment requests, PoS, swap, Dialect notifications, settlement | Live |
| [Phase 2](./phase-2-programmable-payments.md) | SDK + embeddable checkout, gasless payments, agentic payments, white-label, multi-stablecoin, receipts, metrics | Planned |
| [Phase 3](./phase-3-fiat-rails.md) | On/off-ramp, subscriptions, optional ZK-KYC, treasury, tax assistant, security audit | Planned |
| [Phase 4](./phase-4-network-enterprise.md) | Platform integrations, smart routing, enterprise/RBAC, partnerships | Planned |

## Documentation

- [Product Overview](./product-overview.md) — what Secant does and who it serves.
- [How Secant Pay Works](./how-it-works.md) — merchant and customer flow with annotated dapp screenshots.
- [Architecture](./architecture.md) — system design, data flow, and settlement model.
- [Phase 1: Current Build](./phase-1-current-build.md) — features shipped in the current release.
- [Phase 2: Programmable Payments](./phase-2-programmable-payments.md) — SDK, gasless payments, agentic payments, white-label checkout, and merchant tools.
- [Phase 3: Fiat Rails, Recurring & Trust](./phase-3-fiat-rails.md) — on/off-ramp, subscriptions, ZK-KYC, treasury, tax, and the security audit.
- [Phase 4: Network & Enterprise](./phase-4-network-enterprise.md) — platform integrations, smart routing, enterprise/RBAC, and partnerships.
- [Integrations](./integrations.md) — ecosystem providers powering Secant.
- [Security and Settlement](./security-and-settlement.md) — custody model, validation, and operational controls.
- [Contributing](./contributing.md) — how to contribute to docs and code.
