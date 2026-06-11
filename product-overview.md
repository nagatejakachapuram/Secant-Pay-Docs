# Product Overview

Secant Pay is a payment operating system for merchants who work across Base and Solana.

The product combines checkout, invoices, point-of-sale payments, portfolio visibility, and swap routing into one self-custodial workflow. A merchant connects an EVM wallet and a Solana wallet, creates payment requests, shares a payment link or QR code, and tracks settlement without giving Secant custody over funds.

## Core Jobs

### Accept Payments

Merchants can request USDC on Base or Solana. Customers can scan a QR code, open a payment link, or pay from a Solana Action/Blink where supported.

### Receive USDC

Base payments settle directly to the merchant EVM address. Solana checkout can accept SOL or SPL tokens and route through Jupiter so the merchant receives USDC.

### Track Settlement

Secant tracks payment state through on-chain data, Zerion activity, Solana references, and Helius webhook events.

### Manage Invoices

Invoices become shareable payment links. On Solana, invoice links can also expose Action endpoints so they unfurl as payable cards in clients that support Blinks.

### Swap and Bridge

Solana-to-Solana swaps route through Jupiter. EVM swaps and bridge routes use Zerion-powered routing and portfolio data.

## Current Audience

Secant is built for:

- Freelancers and agencies receiving crypto payments.
- Global merchants that prefer stablecoin settlement.
- Solana-native teams that want Blinks, Solana Pay, and Jupiter checkout.
- EVM users who still need portfolio visibility and Base USDC payments.

## Product Principles

- **Self-custodial**: wallets sign directly, and funds settle to merchant-owned addresses.
- **Two-chain first**: Base and Solana are treated as first-class rails.
- **USDC-centered**: checkout and settlement are optimized around stablecoin payments.
- **Composable**: routing, balances, settlement, names, and Blinks use ecosystem-standard providers.

