# Phase 1: Current Build

Phase 1 is the product that is already built in the current Secant workspace.

## Wallets

- EVM wallet connection for Base and other EVM activity through the connected address.
- Solana Wallet Adapter and Wallet Standard support for wallets such as Phantom, Solflare, Backpack, and Jupiter Mobile.
- Separate EVM and Solana wallet identity in the header and checkout surfaces.
- Dashboard balance scope for All wallets, EVM wallet, and Solana wallet.

## Dashboard

- Aggregated portfolio balance across connected wallets.
- Balance chart across wallet scopes.
- Asset list and network distribution from portfolio provider data.
- Activity entry points for payment history and settlement tracking.

## Terminal

- USDC checkout terminal.
- Base and Solana chain selector.
- Receive and send modes.
- QR generation for merchant payment requests.
- Chain identity shown beside the checkout asset so reviewers can see the active rail.

## Scan & Pay

- Point-of-sale screen for scanning or pasting payment payloads.
- Base USDC and Solana Pay support.
- Active-chain payment tabs.
- Max USDC balance display for the selected rail.
- Amount keypad and amount validation against the connected wallet balance.
- Manual paste fallback for QR contents.

## Invoices

- Invoice creation and status tracking.
- Base payment links for EVM USDC checkout.
- Solana payment links for Solana Pay checkout.
- Solana Actions endpoint for invoice Blinks.
- Copy and share actions for invoice payment links.

## Swap & Bridge

- Solana-to-Solana quotes routed through Jupiter.
- EVM swaps and bridge routes routed through Zerion.
- Same-token selection protection in the UI.
- Minimum received and slippage controls shown before signing.

## Solana-Native Features

- Jupiter checkout route so customers can pay with SOL or supported SPL tokens while the merchant receives USDC.
- Solana Pay URL generation with references and memo support.
- Helius webhook endpoint for native Solana settlement detection.
- SNS `.sol` recipient resolution.
- SPL token transfers through `@solana/spl-token`.
- Compute budget priority fee support for more reliable Solana transactions.

## Testnet Support

- Mainnet and testnet toggle.
- Base Sepolia for EVM testing.
- Solana Devnet for Solana testing.
- Native Solana devnet settlement coverage through Helius rather than relying only on EVM-first indexing.

