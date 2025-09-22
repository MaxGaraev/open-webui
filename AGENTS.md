# Repository Guidelines

## Project Structure & Module Organization
Open WebUI combines a SvelteKit UI and a FastAPI service. Front-end sources are in `src/`: `routes/` pages, `lib/` shared UI/state, and `static/` global assets. Backend logic lives in `backend/open_webui/` with `routers/` for endpoints, `models/` plus `migrations/` for persistence, and `retrieval/` for RAG helpers. Environment manifests sit in `docker-compose.*`, `kubernetes/`, and helper scripts under `scripts/`. UI automation resides in `cypress/`, and sample documents for RAG tests live in `test/test_files/`.

## Build, Test & Development Commands
Install toolchains with `npm install` (Node ≥18.13) and `pip install -r backend/requirements.txt` (Python 3.11). Run the UI via `npm run dev`, start the API with `cd backend && ./dev.sh`, and sync Pyodide assets through `npm run pyodide:fetch` when building offline tools. Produce production bundles using `npm run build`, preview with `npm run preview`, and manage Docker workflows through `make install`, `make start`, and `make stop`.

## Coding Style & Naming Conventions
Apply Prettier defaults (two-space indent, trailing commas) and keep Svelte components PascalCase (`ChatPane.svelte`). Shared TypeScript utilities favour camelCase exports; stores belong in `src/lib`. Python modules remain snake_case with 4-space indents. Run `npm run lint` before committing; it chains ESLint, `svelte-check`, and `pylint backend/`. Use `npm run format` for JS/TS/Svelte and `npm run format:backend` to invoke Black.

## Testing Guidelines
Use `npm run test:frontend` to cover Vitest unit and component suites, and `npm run cy:open` for Cypress specs under `cypress/e2e`. Backend checks rely on Pytest; execute `pytest backend/open_webui/test` and name new fixtures or specs `test_*.py`. Integration helpers belong in `backend/open_webui/test/util`, which already wraps Dockerised dependencies.

## Commit & Pull Request Guidelines
Adopt the Conventional Commit prefix seen in history (`feat:`, `fix:`, `chore:`). Subjects stay imperative and ≤72 characters; reference issues in the body (e.g., `Fixes #123`) and mention migrations or API contracts. PRs should summarise intent, list manual verification (`npm run lint`, `npm run build`, target tests), and attach screenshots or API traces when UI or endpoint behaviour changes. Request reviewers who own the affected surface (frontend, backend, infra).

## Security & Configuration Tips
Keep secrets out of version control; rely on local `.env` files consumed by `backend/dev.sh` or the compose stacks. Review `backend/config.py` when adding settings so defaults and validation are aligned, and document any new env vars in the PR description.
