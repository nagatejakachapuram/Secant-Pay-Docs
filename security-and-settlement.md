# Security and Settlement

Secant is designed as a self-custodial payment product. The application coordinates payment requests, routing, and settlement tracking, but wallets sign transactions directly and funds settle to merchant-controlled addresses.

## Custody Model

Secant does not:

- Hold private keys.
- Custody merchant or customer funds.
- Move funds without wallet approval.
- Replace on-chain settlement with internal balances.

Secant does:

- Create payment requests.
- Build transaction payloads for connected wallets.
- Track expected payment amounts and recipients.
- Verify settlement from chain and provider data.
- Store invoice and payment status.

## Payment Validation

A payment should be marked settled only when the observed transaction matches the expected:

- Chain.
- Recipient.
- Asset.
- Amount.
- Invoice or payment reference.
- Transaction status.

## Solana Reliability

Solana transfers use official SPL Token tooling and compute budget priority fee support where relevant. This avoids fragile hand-built instruction byte layouts and improves transaction reliability under congestion.

## Webhook Handling

Webhook events should be treated as settlement signals, not the only source of truth. The backend should validate webhook payloads against expected invoice state and on-chain transaction details before marking a payment settled.

## Testnet Mode

Testnet mode should use Base Sepolia and Solana Devnet. Solana settlement detection should use native Solana infrastructure so reviewers can test payments without depending on EVM-first indexer coverage.

## Operational Controls

Recommended controls:

- Idempotent settlement updates.
- Webhook replay handling.
- Invoice expiration.
- Explicit chain and asset display in every checkout.
- Error states for wrong chain, insufficient balance, and same-token swaps.
- Audit logs for settlement transitions.

