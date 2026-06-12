# Phase 1: Current Build

Phase 1 is the product that is live in the current Secant workspace. Everything listed here is built and functional.

## Wallets

- EVM wallet connection for Base and other EVM activity through injected providers (MetaMask, Coinbase Wallet, Rabby).
- Solana Wallet Adapter and Wallet Standard support for Phantom, Solflare, Backpack, and Jupiter Mobile.
- Separate EVM and Solana wallet identity displayed in the header and across all checkout surfaces.
- Dashboard balance scope selector: All wallets, EVM wallet, or Solana wallet.

## Dashboard

- Aggregated portfolio balance across all connected wallets.
- Balance chart with wallet scope filtering.
- Asset list and network distribution from portfolio provider data.
- Activity entry points for payment history and settlement tracking.

## Terminal Checkout

- USDC checkout terminal with configurable amount.
- Base and Solana chain selector with active rail indicator.
- Receive mode: generates QR code and payment link for customers to pay.
- Send mode: transfer USDC from connected wallet.
- Solana Pay URL encoding with recipient, amount, SPL token mint, reference keypair, and memo.
- Payment status polling with exponential backoff on errors.
- Chain identity shown beside the checkout asset so the active rail is always visible.

## Scan & Pay (Point of Sale)

- Point-of-sale screen for merchant-facing payment collection.
- QR scanning and manual paste fallback for payment payloads.
- Base USDC and Solana Pay support with active-chain tabs.
- Max USDC balance display for the selected rail.
- Amount keypad with validation against connected wallet balance.
- Chain-aware transaction building and signing.

## Invoices

- Invoice creation with amount, chain, and recipient configuration.
- Unique invoice ID generation (`inv_` + cryptographically random hex).
- Base payment links for EVM USDC checkout.
- Solana payment links for Solana Pay checkout.
- Solana Actions endpoint exposing invoice metadata for Blinks — invoices unfurl as payable cards in compatible clients.
- Copy and share actions for payment links.
- Invoice status tracking: PENDING, SETTLED, EXPIRED, FAILED.
- 30-minute invoice expiry enforced at both creation and settlement time.

## Swap & Bridge

- Solana-to-Solana swap quotes routed through Jupiter.
- EVM swap and bridge routes routed through Zerion.
- Same-token selection protection in the UI.
- Minimum received amount and slippage controls shown before signing.
- Route and price impact visibility.

## Solana-Native Features

- Jupiter checkout routing: customers pay with SOL or supported SPL tokens, merchant receives USDC.
- Solana Pay URL generation with reference keypairs and memo support.
- Helius webhook endpoint for native Solana settlement detection on both devnet and mainnet.
- SNS `.sol` recipient name resolution.
- SPL token transfers through `@solana/spl-token` with proper associated token account handling.
- Compute budget priority fee support for reliable transaction landing under congestion.

## Settlement

- Backend validates every settlement against stored invoice state: chain, recipient, asset, amount, and reference must all match.
- Atomic settlement via DynamoDB `TransactWriteItems` — settlement marker and invoice update succeed or fail together.
- Settlement marker rows prevent double-settlement of the same on-chain transaction.
- Consistent reads on invoice lookups during settlement validation.
- Invoice expiry checked before settlement processing.

## API Security

- Bearer token authentication on all backend endpoints.
- Strict JSON schema enforcement — `DisallowUnknownFields()` rejects payloads with unexpected fields.
- Provider API keys isolated to server-side Next.js API routes, never exposed to browser.
- RPC proxy with response sanitization to prevent API key leakage through error messages.
- Structured error codes and typed error responses across all endpoints.

## Testnet Support

- Mainnet and testnet environment toggle.
- Base Sepolia for EVM testing.
- Solana Devnet for Solana testing.
- Native Solana devnet settlement coverage through Helius rather than relying on EVM-first indexer coverage.
