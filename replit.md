# Keyword Density Checker

An SEO utility that analyzes pasted content or public webpages for keyword frequency, phrase usage, and density.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/keyword-density-checker/src/pages/home.tsx` — main analyzer experience and report UI
- `artifacts/keyword-density-checker/src/index.css` — shared visual theme and motion utilities
- `artifacts/api-server/src/routes/keyword-density.ts` — text analysis and public URL extraction
- `lib/api-spec/openapi.yaml` — source of truth for the analysis API contract

## Architecture decisions

- Analysis is stateless and does not persist submitted text or URLs.
- Public URL extraction is handled server-side to avoid browser CORS restrictions.
- Keyword density is calculated against total words, while stop-word filtering only changes which terms are surfaced.

## Product

- Paste text or enter a public URL.
- Review total words, unique words, sentences, paragraphs, reading time, keyword density, and phrase frequency.
- Toggle phrase analysis and stop-word inclusion.
- Copy a short source preview from the report.

## User preferences

No standing preferences recorded.

## Gotchas

- Public URL scans require a reachable HTTP(S) page with readable text.
- Regenerate API clients after changing `lib/api-spec/openapi.yaml`.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
