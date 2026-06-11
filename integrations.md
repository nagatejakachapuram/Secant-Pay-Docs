# Integrations

Secant is powered by ecosystem integrations that handle portfolio data, routing, settlement detection, and payment standards.

## Zerion

Zerion powers EVM portfolio data, chain activity, and EVM swap or bridge routing.

Current uses:

- EVM wallet portfolio balances.
- Position and asset metadata.
- Transaction history.
- Chain metadata.
- EVM swap and bridge route discovery.

## Jupiter

Jupiter powers Solana liquidity and swap execution.

Current uses:

- Solana-to-Solana swap quotes.
- Checkout routing from SOL or SPL tokens into merchant USDC.
- Minimum received calculation before signing.
- Route and price impact visibility.

## Solana Pay

Solana Pay powers QR and link-based payment requests on Solana.

Current uses:

- Payment URL generation.
- Recipient, amount, SPL token, reference, and memo encoding.
- QR checkout flows.
- Manual paste fallback for payment payloads.

## Solana Actions and Blinks

Solana Actions expose invoice payment endpoints that can unfurl into payable cards in clients that support Blinks.

Current uses:

- Invoice action metadata.
- Payment transaction generation.
- Shareable Solana payment cards.

## Helius

Helius powers native Solana webhook settlement detection.

Current uses:

- Devnet-capable Solana payment observation.
- Mainnet Solana payment event delivery.
- Reference-based settlement tracking.

## SNS

SNS resolves `.sol` names for more human-friendly Solana recipients.

Current uses:

- Recipient input resolution.
- Merchant and customer address convenience.

## Wallet Standard and Solana Wallet Adapter

Wallet Standard and Solana Wallet Adapter allow Secant to connect to a broad set of Solana wallets instead of relying on `window.solana`.

Current uses:

- Phantom.
- Solflare.
- Backpack.
- Jupiter Mobile.
- Other Wallet Standard-compatible Solana wallets.

