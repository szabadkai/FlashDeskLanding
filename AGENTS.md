# Repository Guidelines

## Project Structure & Module Organization
- Root: docs and configs (e.g., `README_*`, `DEPLOYMENT.md`, `specs.md`). Support folders: `.claude/`, `.playwright-mcp/`, `.history/`.
- `web/`: Vite-powered web client (`index.html`, `js/`, `styles/`, `overlay/`, `dist/`).
- `server/`: Node WebSocket signaling server (`server/src/index.js`).
- `scripts/`, `host/`, `jamf-profiles/`: operational assets and helpers.
- Tests (when added): place under `tests/` mirroring source paths (e.g., `web/js/ui.js` → `tests/web/js/ui.test.js`).

## Build, Test, and Development Commands
- Prerequisite: Node >= 18 installed.
- Web:
  - `cd web && npm install`
  - `npm run dev` — start local dev server (HMR).
  - `npm run build` — production build to `web/dist`.
  - `npm run preview` — serve built assets (use `--host` to expose).
- Server:
  - `cd server && npm install`
  - `npm run dev` — start with watch.
  - `npm start` — run signaling server.
- Tests: none configured yet. Prefer Vitest for `web/` and Node’s built-in test runner or Vitest for `server/`.
  - Examples: `npx vitest run` (web) or `node --test` (server).

## Coding Style & Naming Conventions
- Indentation 2 spaces; UTF-8; LF; wrap around ~100 chars.
- Keep modules small; one responsibility per file.
- Filenames: scripts `kebab-case`, data `lower_snake_case`, docs `PascalCase`.
- Organize code under `web/js/`, `web/styles/`, and `server/src/` with small, composable APIs.

## Testing Guidelines
- Name tests `*.test.js` or `*.test.ts` and mirror source paths.
- Include at least one happy path and one failure path per unit.
- If enabling coverage, target ≥80% lines/branches.

## Commit & Pull Request Guidelines
- Commits: present-tense, scoped messages (e.g., `feat(web): add theme toggle`, `fix(server): handle stale offers`). Keep atomic.
- PRs: include purpose, summary of changes, trade-offs, testing notes, and linked issues. Add screenshots/recordings for UX-visible updates. Ensure green tests and self-review of `git diff`.

## Security & Configuration Tips
- Never commit secrets. Use local env files (e.g., `web/.env.local`) and update `.gitignore`.
- For TLS, set `SSL_KEY_PATH` and `SSL_CERT_PATH` for the server; never commit key material.
- Prefer least-privilege configs and review dependencies before adding.
