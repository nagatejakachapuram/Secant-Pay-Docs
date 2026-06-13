# Phase 3: Fiat Rails, Recurring & Trust

Phase 3 connects Secant to the off-chain world — fiat in and out, standing payments, and the trust layer that real merchant volume needs. It is also where the independent **security audit** gates production scale.

## On-Ramp

Let customers or merchants acquire USDC without leaving the checkout flow, using established on-ramp partners — the partner carries the licensing and compliance burden, so this is an integration, not a regulated build.

- Card, bank transfer, and local payment methods through partner providers.
- Buy USDC on Base or Solana, delivered to the user's own wallet (the self-custodial flow then runs unchanged).
- Wallet-aware destination selection.
- Regional availability, fees, and limits shown before handoff.
- Merchant-configurable preferred rail.

## Off-Ramp

USDC-to-bank or USDC-to-local-currency payouts for merchants, also via established payout partners.

- Bank-account payout setup through a partner.
- Stablecoin-to-fiat settlement handled by the partner rail.
- Payout status tracking, fee, and ETA display.
- Exportable payout records for accounting.

## Recurring Payments and Subscriptions

Enable subscription billing — the most-requested missing primitive in crypto payments. (It lands here because it changes the trust model: the customer grants standing authority and Secant pulls on a schedule.)

- Merchant creates plans with amount, interval, and trial period.
- Customer approves a token spending cap (ERC-20 approve on Base, token delegation on Solana).
- Secant pulls payments on schedule via backend automation, within the approved cap.
- Failed-payment retry logic with configurable retry count and grace period.
- Subscription lifecycle: active, paused, cancelled, past due, expired.
- Customer self-service portal for managing active subscriptions.
- Usage-based billing with metered events and threshold triggers.
- Dunning management: automated reminders before and after failed charges.

## Optional Privacy-Preserving KYC (ZK)

Optional, merchant-toggled identity verification that proves compliance facts **without exposing raw PII** — so merchants who need compliance get it, and those who don't keep the permissionless flow.

- **ZK proofs of compliance facts:** a customer or merchant proves "over 18", "not on a sanctions list", or "verified in jurisdiction X" via a zero-knowledge proof issued by a KYC provider — Secant never stores identity documents.
- **Pluggable providers:** integrate one or more KYC/identity issuers; merchants choose the provider.
- **Per-flow policy:** KYC required, optional, or off, configured per checkout or payout flow.
- **Reusable credentials:** verify once, reuse the proof across merchants and sessions.
- **Feeds the rails:** on/off-ramp partners that require KYC consume the proof instead of re-collecting documents.

## Risk and Controls

- Optional sanctions-screening provider integration.
- Transaction limits by chain and wallet.
- Suspicious-payment review queue.

## Treasury Management

- Merchant treasury policy rules and auto-sweep to a preferred wallet or chain.
- Stablecoin allocation by chain with rebalancing triggers.
- Optional idle-balance routing to approved yield products.
- FX and stablecoin-exposure reporting.
- Risk limits by wallet, chain, and counterparty.

## Tax Reporting and Compliance Assistant

AI-powered tax reporting that turns Secant transaction history into jurisdiction-aware, filing-ready output. Not tax advice — a reporting tool that already knows the merchant's payment data.

Initial coverage (5 markets with highest crypto-merchant activity):

| Country | Tax Framework | Key Rule |
|---------|--------------|----------|
| United States | IRS — capital gains on disposal, 1099 reporting | Every stablecoin swap is a taxable event; USDC-to-USD is reportable |
| India | 30% flat tax on crypto gains + 1% TDS | Every token swap triggers 30% tax; no loss offset allowed |
| United Kingdom | HMRC — capital gains tax, trading income rules | Crypto payments received as business income taxed as trading profits |
| UAE | No federal income tax, but VAT applies | USDC payments subject to 5% VAT on goods/services |
| Singapore | IRAS — no capital gains tax, but income tax on trading | Payment receipts taxed as business income; no capital gains event on holding |

Scope:

- Automatic taxable-event classification based on the merchant's configured jurisdiction.
- Settlement-level breakdown: which payments are income, which token conversions are disposal events, which are tax-neutral.
- Capital gains/loss calculation where applicable, using cost basis from Secant's own transaction records.
- Tax-ready export: CSV formatted per country's filing system, PDF summary reports.
- Local accounting-tool integration: Tally (India), Xero (UK, AU, Singapore), QuickBooks (US), Zoho Books (UAE, India).
- Natural-language query interface grounded in the merchant's actual Secant data.
- Quarterly and annual report generation on demand.

Design constraints:

- Labeled a "tax reporting assistant", not tax advice; disclaimers on all output.
- Tax rules maintained as structured per-country rule engines, not LLM-generated interpretations.
- AI handles natural-language queries and report formatting; tax classification is deterministic code.

## Security Audit

Independent security review of the backend API and payment infrastructure — the gate before scaling merchant onboarding and before fiat rails carry real volume.

- Webhook signature verification and bearer-token authentication.
- Invoice creation and settlement-matching integrity.
- API input validation and error handling (no secret leakage in responses).
- AWS IAM and DynamoDB access-policy review (least-privilege per Lambda).
- Solana Pay URL construction and SPL-transfer parameter validation.
- Fee-payer relay and gasless-sponsorship paths from Phase 2.
- Merchant-settings wallet-signature authentication (Solana ed25519 / EVM EIP-191 ownership proof, timestamp-bounded against replay).
