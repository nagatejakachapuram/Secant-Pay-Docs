# Phase 2: Growth Rails

Phase 2 should make Secant easier to use for real merchants and more measurable for growth.

## On-Ramp

Add fiat-to-crypto onboarding so customers or merchants can acquire USDC without leaving the checkout flow.

Potential scope:

- Card, bank transfer, and local payment method providers.
- Buy USDC on Base or Solana.
- Wallet-aware on-ramp destination selection.
- Regional availability, fees, and limits shown before handoff.
- Merchant-configurable preferred rail.

## Off-Ramp

Add USDC-to-bank or USDC-to-local-currency payout options for merchants.

Potential scope:

- Bank account payout setup.
- Stablecoin-to-fiat settlement.
- Payout status tracking.
- Fee and ETA display.
- Exportable payout records for accounting.

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

- Hosted checkout pages for each invoice.
- Email or shareable receipt pages.
- Refund workflow.
- Partial payment handling.
- Payment expiration controls.
- Merchant branding controls.
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

