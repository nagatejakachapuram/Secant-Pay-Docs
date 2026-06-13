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
- Customer wallet request field for Solana invoices. When supplied, Secant creates the invoice and sends a Dialect payment request notification to the customer wallet.
- Optional memo field for tagging invoices with context (company name, project, purpose). Memo is stored with the invoice and displayed on the invoice list, payment link, and Blink card.
- Unique invoice ID generation (`inv_` + cryptographically random hex).
- Base payment links for EVM USDC checkout.
- Solana payment links for Solana Pay checkout.
- Secant Blinks: a first-party Solana Action endpoint exposing invoice metadata and building the payment transaction in the Secant backend. Invoices unfurl as payable cards in compatible clients (Secant's own `/pay` checkout, native wallets, and Dialect `dial.to` as the shareable web renderer). Only the payer account is caller-supplied — recipient, amount, mint, and reference come from the stored invoice. When a memo is set, it appears in the Blink title and description.
- Copy and share actions for payment links.
- Copy Blink URL action for Solana invoices. Blink rendering depends on the receiving client or renderer; the Secant backend remains the transaction builder.
- Invoice status tracking: PENDING, SETTLED, EXPIRED, FAILED.
- Settled invoices remain visible in the merchant list and cannot be hidden from the local invoice list UI.
- 30-minute invoice expiry enforced at both creation and settlement time.

## Notifications (Dialect Alerts)

- Dialect Alerts integration: when a merchant supplies a customer wallet on a Solana invoice, the backend sends an in-app payment-request alert to that wallet, carrying the invoice amount, memo, and pay link.
- First-connect opt-in: connecting a Solana wallet prompts the merchant to enable notifications and sign a one-time message that subscribes them to Secant's Dialect app.
- In-app inbox in the dashboard notification bell — an anchored dropdown on desktop and a bottom-sheet on mobile — for reviewing received requests and settlement alerts.
- The Dialect API key stays server-side; the browser uses only the public dapp address and the publishable client key.
- Delivery requires the recipient wallet to be subscribed to Secant's Dialect app. Dialect Alerts are a request surface and never settle invoices — settlement remains the backend's authority.

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
- Helius webhook settlement verified on mainnet with invoice status changing from `PENDING` to `SETTLED` after payment.
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

- Per-endpoint authentication: bearer token on invoice initiation, HMAC signature on the settlement webhook, constant-time static bearer on the Helius webhook, RSA signature on the Zerion webhook. Public payment-surface endpoints (invoice details, Blink action, Jupiter checkout) are intentionally unauthenticated — they expose only payable data and build unsigned transactions the payer signs.
- Strict JSON schema enforcement — `DisallowUnknownFields()` rejects payloads with unexpected fields.
- Provider API keys isolated to server-side Next.js API routes, never exposed to browser.
- RPC proxy with response sanitization to prevent API key leakage through error messages.
- Structured error codes and typed error responses across all endpoints.

## Testnet Support

- Mainnet and testnet environment toggle.
- Base Sepolia for EVM testing.
- Solana Devnet for Solana testing.
- Native Solana devnet settlement coverage through Helius rather than relying on EVM-first indexer coverage.
