# Secant Pay Docs

This folder is a self-contained GitBook-ready documentation workspace for Secant Pay. It can be moved into its own repository without depending on the app, backend, or SDK folders.

Secant Pay is a self-custodial crypto payments workspace for merchants who want Base and Solana payments, portfolio visibility, invoices, point-of-sale checkout, and swap/bridge routing in one product.

The current product focuses on two payment rails:

- **Base** for EVM USDC payments, EVM wallet connectivity, and Zerion-powered portfolio and routing data.
- **Solana** for Solana Pay, Wallet Standard wallets, Jupiter-powered swaps, SPL token checkout, Blinks, SNS names, and native settlement detection.

Secant does not custody funds or private keys. Customers pay directly from their wallet, merchants receive into their own connected wallet, and the product tracks payment state around those on-chain transfers.

## What is in Phase 1

Phase 1 is the current build:

- Multi-wallet dashboard for EVM and Solana wallets.
- Aggregated portfolio balances across connected wallets.
- Terminal checkout for Base and Solana.
- Scan & Pay point of sale for Base USDC and Solana Pay.
- Invoices with Base links and Solana Blinks.
- Swap & Bridge with Jupiter for Solana swaps and Zerion for EVM swaps and bridges.
- Solana Wallet Adapter / Wallet Standard support.
- SNS `.sol` resolution.
- Helius webhook support for Solana settlement.
- SPL token transfers through `@solana/spl-token` with compute budget priority fees.

## Docs Map

- [Product Overview](./product-overview.md)
- [Architecture](./architecture.md)
- [Phase 1: Current Build](./phase-1-current-build.md)
- [Phase 2: Growth Rails](./phase-2-growth-rails.md)
- [Phase 3: Advanced Network](./phase-3-advanced-network.md)
- [Integrations](./integrations.md)
- [Security and Settlement](./security-and-settlement.md)
