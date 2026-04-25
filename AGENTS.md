# AGENTS

## Scope
- This repository is a Bun monorepo with two active apps:
  - `apps/api`: Bun + Elysia backend
  - `apps/web`: Vue + Vite frontend
- Prefer app-local changes. Avoid cross-app refactors unless requested.

## First Read
- Root overview: [README.md](README.md)
- API docs: [apps/api/README.md](apps/api/README.md)
- Web docs: [apps/web/README.md](apps/web/README.md)

## Working Directories
- Run API commands from `apps/api`.
- Run Web commands from `apps/web`.
- Run dependency install from repo root.

## Commands
- Install dependencies (root): `bun install`
- API dev server (`apps/api`): `bun run dev` (serves on `http://localhost:3000`)
- Web dev server (`apps/web`): `bun dev` (serves on `http://localhost:5173`)
- Web build (`apps/web`): `bun run build`
- Web unit tests (`apps/web`): `bun test:unit`
- Web e2e tests (`apps/web`): `bun test:e2e`

## Test Expectations
- If you change `apps/web/src/**`, run `bun test:unit` in `apps/web`.
- If you change `apps/web/e2e/**` or routing/app boot logic, run `bun test:e2e` in `apps/web`.
- API currently has no real test suite configured; avoid adding fake passing tests.

## Project Conventions
- Keep API entry and server setup in [apps/api/src/index.ts](apps/api/src/index.ts).
- Use `@/` imports for web source modules (configured in [apps/web/vite.config.ts](apps/web/vite.config.ts) and [apps/web/tsconfig.app.json](apps/web/tsconfig.app.json)).
- Follow existing Vue patterns:
  - Router setup in [apps/web/src/router/index.ts](apps/web/src/router/index.ts)
  - Pinia stores in [apps/web/src/stores/counter.ts](apps/web/src/stores/counter.ts)
- Web formatting uses `oxfmt` via `bun run format` in `apps/web`.

## Known Pitfalls
- Web app uses Vue beta packages (see `overrides` in [apps/web/package.json](apps/web/package.json)); avoid version drift changes unless requested.
- Playwright behavior changes on CI (`CI` env): base URL/port and retries differ. See [apps/web/playwright.config.ts](apps/web/playwright.config.ts).
- Root `README.md` still contains Bun init boilerplate command (`bun run index.ts`), which does not reflect current monorepo scripts.

## Change Boundaries
- Do not introduce new frameworks, linters, or formatters without explicit request.
- Do not move files across app boundaries without explicit request.
- Keep edits focused and minimal; preserve existing config style.