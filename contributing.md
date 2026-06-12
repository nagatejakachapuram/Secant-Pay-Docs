# Contributing

Secant Pay is organized as a monorepo workspace. Contributions to documentation, frontend, backend, and SDK each follow the conventions below.

## Repository Structure

```text
Secant/
  Secant-Pay/
    Secant-frontend/       Next.js 14 — App Router, API routes, UI components
    Secant-backend/        Go — invoice lifecycle, settlement, webhooks
  Secant-SDK/              TypeScript — payment intents, status, embeddable checkout
  Secant Pay docs/         GitBook documentation
```

## Documentation

Docs live in `Secant Pay docs/` at the workspace root. This directory is a self-contained GitBook workspace — it can be moved to its own repository without depending on the app, backend, or SDK.

- `README.md` is the docs home page.
- `SUMMARY.md` controls the GitBook sidebar.
- Product, architecture, roadmap, integrations, and security pages are separate topic files.

### Doc Style

- Keep pages short and scannable.
- Use direct product language — write what the system does, not what it might do.
- Phase 1 content covers only features already built and functional.
- Roadmap ideas belong in Phase 2 or Phase 3.
- Use Mermaid for architecture and flow diagrams.
- Use tables for structured comparisons and specifications.

## Frontend

The frontend is a Next.js 14 application using the App Router.

| Area | Convention |
|------|-----------|
| Components | `components/` directory, one component per file |
| API routes | `app/api/` directory, server-side only — no client-side secrets |
| Styling | Tailwind CSS |
| Wallet connection | EVM injected providers + Solana Wallet Adapter |
| Environment variables | `NEXT_PUBLIC_` prefix for browser-safe values only. Provider API keys use non-public env vars and are accessed through API routes |

## Backend

The backend is written in Go with a focus on correctness and minimal dependencies.

| Area | Convention |
|------|-----------|
| Package structure | `internal/backend/` for core logic, `cmd/` for entry points |
| JSON handling | `DisallowUnknownFields()` on all decoders — strict schema enforcement |
| Error handling | Typed `AppError` with HTTP status codes, no leaked internal details |
| Storage | `InvoiceStore` interface with DynamoDB and in-memory implementations |
| Testing | Table-driven tests, in-memory store for unit tests |
| Deployment | Designed for AWS Lambda or standalone HTTP — stateless handlers |

## Code Quality

- No provider API keys in client-side code or console output.
- No `console.log` / `console.error` in production API routes that could leak sensitive data.
- Structured error responses on all endpoints — no raw error strings to clients.
- Conditional writes on all database mutations — no optimistic overwrite patterns.

## GitBook Configuration

The `.gitbook.yaml` at the docs root configures GitBook to use `README.md` as the homepage and `SUMMARY.md` as the sidebar. GitBook also supports the `?ask=<question>` query parameter on any page for AI-powered doc search.
