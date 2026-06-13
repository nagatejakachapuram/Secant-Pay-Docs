# Phase 2: Programmable Payments

Phase 2 turns Secant from a merchant app into a developer platform for **programmable, autonomous payments**. The theme: anything that can hold a wallet — a web app, a backend script, or an AI agent — can accept or make a Secant payment, and no one needs to hold a native gas token to do it.

## Secant SDK and Embeddable Checkout

Publish a TypeScript SDK (`@secant-pay/sdk`) that lets any developer integrate Secant without building payment flows from scratch. The SDK is the foundation the rest of Phase 2 — and the integrations in Phase 4 — build on.

SDK scope:

- `createPaymentIntent(amount, chain, options)` returns an invoice object with payment URL, QR data, Blink URL, and a status-polling handle.
- `sendPaymentRequest(invoiceId, customerWallet)` sends a wallet-addressed request through supported notification channels (Dialect today).
- `getPaymentStatus(invoiceId)` returns the current settlement state.
- `verifyWebhookSignature(payload, secret)` helper for backend webhook consumers.
- Embeddable `<SecantCheckout />` React component that renders a connect-wallet checkout inside any page.
- Framework-agnostic web component (`<secant-checkout>`) for non-React apps.
- WebSocket or SSE subscription for real-time payment-status updates.
- Full TypeScript types for every request and response shape.

## Agentic Payments

Let AI agents and automated services **pay invoices and execute Blinks programmatically**, within scoped, capped spending authority. This builds directly on the Phase 1 Action API (Secant Blinks) — the same endpoint that turns an invoice into a signable transaction with only the payer supplied is exactly the shape a machine payer needs.

Scope:

- **Agent-friendly payment intents:** an agent fetches an invoice's Action metadata, has the transaction assembled server-side, and submits it with its own delegated key — no human UI required.
- **Scoped spending authority:** per-agent spending caps, allow-listed recipients/merchants, and time-bounded approvals, so an agent can pay autonomously *only* within limits the owner sets.
- **HTTP-native (x402-style) payments:** respond to an `HTTP 402 Payment Required` with a Secant Blink/invoice the agent settles, then unlock the resource — pay-per-call APIs and machine-metered services.
- **Machine-to-machine settlement:** agents paying agents; usage-based services billing per request.
- **Programmatic Blink execution** through the SDK: discover, build, sign, submit, and confirm a Blink end to end in code.
- **Reconciliation:** every agent payment carries the invoice ID, an agent identity, and the on-chain signature, so autonomous spend is fully auditable.

Why this is a Phase 1 extension, not a new system: Secant already builds invoice-addressed, payer-only transactions in the backend. Agentic payments add the *authority model* (caps, allow-lists) and the *programmatic surface* (SDK), not a new settlement path.

## Gasless Payments

Remove the requirement for customers to hold native tokens (ETH or SOL) to complete a payment.

Base (EVM):

- Integrate an ERC-4337 Paymaster so customers sign a USDC transfer and gas is sponsored.
- Coinbase Paymaster integration for Base mainnet.
- Merchant-configurable sponsorship: merchant pays, customer pays, or Secant subsidizes.
- Gas cost shown transparently before signing.

Solana:

- Fee-payer relay service where Secant submits the transaction and pays the SOL fee.
- Customer signs only the USDC transfer instruction.
- Fee recovered from the payment amount or absorbed by merchant config.

> **Security note:** the fee-payer relay holds keys and SOL to sponsor transactions, so it is the one Phase 2 component that touches funds directly. Give it a focused security review before production, ahead of the full independent audit in Phase 3.

## White-Label & Custom-Domain Checkout

Phase 1 already ships public pay pages at `/pay/{invoice_id}`. Phase 2 expands them into fully branded, merchant-owned checkout that works without the Secant dashboard.

- **Custom domains:** `pay.merchant.com` or `pay.secant.so/{invoice_id}`.
- **Full white-label branding:** name, logo, brand color, support link, custom message, and an option to remove Secant identity entirely.
- Mobile-first hosted pages with wallet-handoff fallbacks; no app install required.
- Customers pay via Solana Pay QR, wallet connect, Blink-compatible clients, or manual transfer.
- Live payment status on the page after submission.
- Conversion and abandonment tracking per delivery channel: QR, pay link, Blink, and notification request.

## Multi-Stablecoin Acceptance

Accept stablecoins beyond USDC at checkout while merchants still receive their preferred settlement token.

- Accept USDT, PYUSD, DAI, and EURC at checkout.
- Auto-convert to the merchant's preferred stablecoin via Jupiter (Solana) or Zerion (Base) routing.
- Merchant configures accepted tokens and preferred settlement token in dashboard settings.
- Customer sees available payment tokens and the conversion rate before signing.
- Conversion fee and slippage shown transparently.

## On-Chain Payment Receipts

Generate verifiable payment proofs that exist independently of Secant infrastructure.

- After settlement, generate a signed receipt with invoice ID, amount, payer, recipient, tx hash, and timestamp.
- Base: publish an attestation via the Ethereum Attestation Service (EAS).
- Solana: publish via on-chain memo or an attestation program.
- Receipt verifiable by any third party without calling Secant APIs.
- Exportable receipt page with a QR code linking to the on-chain proof.
- Strengthens the self-custodial claim: payment state is not locked inside Secant's database.

## Merchant Metrics

- Gross payment volume; successful, failed, and expired payment rates.
- Average settlement time; chain split by Base and Solana.
- Payment-method split by QR, invoice, Blink, terminal, and agent.
- USDC received by period; repeat-payer count.
- Quote acceptance rate, average slippage, and routing fee for swap/multi-stablecoin checkout.
- Active, overdue, and aging invoices.

## Accounting

- CSV exports.
- QuickBooks and Xero export targets.
- Invoice and payout reconciliation.
- Per-chain settlement report.
- Audit log for payment state changes.
