# Phase 2: Growth Rails

Phase 2 makes Secant usable for real merchants, adoptable by developers, and measurable for growth.

## Secant SDK and Embeddable Checkout

Publish a TypeScript SDK (`@secant-pay/sdk`) that lets any developer integrate Secant into their app without building payment flows from scratch.

SDK scope:

- `createPaymentIntent(amount, chain, options)` returns an invoice object with payment URL, QR data, and status polling handle.
- `sendPaymentRequest(invoiceId, customerWallet)` sends a wallet-addressed request through supported notification channels.
- `getPaymentStatus(invoiceId)` returns current settlement state.
- `verifyWebhookSignature(payload, secret)` helper for backend webhook consumers.
- Embeddable `<SecantCheckout />` React component that renders a connect-wallet checkout flow inside any page.
- Framework-agnostic web component (`<secant-checkout>`) for non-React apps.
- WebSocket or SSE subscription for real-time payment status updates.
- Full TypeScript types for all request and response shapes.

The SDK is the foundation for Phase 3 integrations. Shopify, WooCommerce, and bot integrations will consume the SDK rather than raw API calls.

## Hosted Payment Link Improvements

Phase 1 already ships public invoice pay pages at `/pay/{invoice_id}`. Phase 2 expands them into merchant-branded, higher-conversion checkout pages that work without the merchant dashboard.

Scope:

- Custom domain support such as `pay.secant.so/{invoice_id}` or merchant-owned payment domains.
- Merchant profile: name, logo, brand color, support link, and custom message.
- Works on mobile browsers without app install, including wallet handoff fallbacks.
- Customer can pay via Solana Pay QR scan, wallet connect, Blink-compatible clients, or manual transfer.
- Merchant can share links via email, social media, messaging, or embedded in websites.
- Payment status updates live on the page after transaction submission.
- Conversion and abandonment tracking for each delivery channel: QR, pay link, Blink, and notification request.

## Gasless Payments

Remove the requirement for customers to hold native tokens (ETH or SOL) to complete a payment.

Base (EVM):

- Integrate ERC-4337 Paymaster so customers sign a USDC transfer and gas is sponsored.
- Coinbase Paymaster integration for Base mainnet.
- Merchant-configurable gas sponsorship: merchant pays, customer pays, or Secant subsidizes.
- Gas cost shown transparently before signing.

Solana:

- Fee-payer relay service where Secant submits the transaction and pays the SOL fee.
- Customer signs only the USDC transfer instruction.
- Fee recovered from the payment amount or absorbed by merchant config.

## Multi-Stablecoin Acceptance

Accept stablecoins beyond USDC at checkout while merchants still receive their preferred settlement token.

Scope:

- Accept USDT, PYUSD, DAI, and EURC at checkout.
- Auto-convert to merchant's preferred stablecoin via Jupiter (Solana) or Zerion (Base) routing.
- Merchant configures accepted tokens and preferred settlement token in dashboard settings.
- Customer sees available payment tokens and conversion rate before signing.
- Conversion fee and slippage shown transparently.

## On-Ramp

Add fiat-to-crypto onboarding so customers or merchants can acquire USDC without leaving the checkout flow.

Scope:

- Card, bank transfer, and local payment method providers.
- Buy USDC on Base or Solana.
- Wallet-aware on-ramp destination selection.
- Regional availability, fees, and limits shown before handoff.
- Merchant-configurable preferred rail.

## Off-Ramp

Add USDC-to-bank or USDC-to-local-currency payout options for merchants.

Scope:

- Bank account payout setup.
- Stablecoin-to-fiat settlement.
- Payout status tracking.
- Fee and ETA display.
- Exportable payout records for accounting.

## On-Chain Payment Receipts

Generate verifiable payment proofs that exist independently of Secant infrastructure.

Scope:

- After settlement, generate a signed receipt containing invoice ID, amount, payer, recipient, tx hash, and timestamp.
- Base: publish attestation via Ethereum Attestation Service (EAS).
- Solana: publish attestation via on-chain memo or attestation program.
- Receipt verifiable by any third party without calling Secant APIs.
- Exportable receipt page with QR code linking to on-chain proof.
- Strengthens the self-custodial claim: payment state is not locked inside Secant's database.

## Merchant Metrics

Add metrics that help merchants understand conversion, settlement, and revenue quality.

Recommended metrics:

- Gross payment volume.
- Successful payment rate.
- Failed or expired payment rate.
- Average settlement time.
- Chain split by Base and Solana.
- Payment method split by QR, invoice, Blink, and terminal.
- USDC received by period.
- Quote acceptance rate for swap checkout.
- Average slippage and routing fee.
- Repeat payer count.
- Active invoices, overdue invoices, and invoice aging.

## Checkout Improvements

- Email or shareable receipt pages.
- Refund workflow with on-chain tracking.
- Partial payment handling and underpayment detection.
- Payment expiration controls.
- Customer-facing payment status page.

## Accounting

- CSV exports.
- QuickBooks and Xero export targets.
- Invoice reconciliation.
- Payout reconciliation.
- Per-chain settlement report.
- Audit log for payment state changes.

## Risk and Controls

- Optional sanctions screening provider integration.
- KYB/KYC provider hooks for merchants that require compliance.
- Transaction limits by chain and wallet.
- Suspicious payment review queue.
- Team member permissions and approval controls.
