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
| [Phase 1](./phase-1-current-build.md) | Core checkout, invoices, payment requests, PoS, swap, settlement | Live |
| [Phase 2](./phase-2-growth-rails.md) | SDK, hosted payment links, gasless payments, on/off-ramp, multi-stablecoin, metrics | Planned |
| [Phase 3](./phase-3-advanced-network.md) | Subscriptions, platform integrations, smart routing, treasury, enterprise | Planned |

## Documentation

- [Product Overview](./product-overview.md) — what Secant does and who it serves.
- [How Secant Pay Works](./how-it-works.md) — merchant and customer flow with annotated dapp screenshots.
- [Architecture](./architecture.md) — system design, data flow, and settlement model.
- [Phase 1: Current Build](./phase-1-current-build.md) — features shipped in the current release.
- [Phase 2: Growth Rails](./phase-2-growth-rails.md) — SDK, gasless payments, payment links, and merchant tools.
- [Phase 3: Advanced Network](./phase-3-advanced-network.md) — subscriptions, integrations, routing, and enterprise.
- [Integrations](./integrations.md) — ecosystem providers powering Secant.
- [Security and Settlement](./security-and-settlement.md) — custody model, validation, and operational controls.
- [Contributing](./contributing.md) — how to contribute to docs and code.
