# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `e6446b9` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
split wise is a Quorq-generated split-wise calculator consisting of two independently run applications in one repo: a Vite + React 19 single-page frontend containing the approved, reviewed screens (currently rendering seeded sample data, not yet wired to the API), and a FastAPI 0.115 backend that has no approved architecture yet and therefore exposes only a health-check endpoint. The backend uses SQLAlchemy with a SQLite database by default (swappable via DATABASE_URL to Postgres, matching the approved stack) and ships a Dockerfile; the frontend uses Tailwind CSS, React Router, Vitest, and Playwright.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for npm/Vite 6, React 19, TypeScript 5.6)
- Python 3.12 (per backend/Dockerfile)
- pip
- Docker and docker-compose (optional, for the Postgres 16 container defined in docker-compose.yml)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. git clone <repo> and cd into it
2. cp .env.example .env and fill in any values it defines
3. cd frontend && npm install
4. cd backend && pip install -r requirements.txt
5. (optional) from the repo root, run docker-compose up -d to start a local Postgres 16 instance, then set DATABASE_URL to point the backend at it instead of the default SQLite file
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| frontend dev | `cd frontend && npm run dev` | Starts the Vite dev server for the SPA (defaults to http://localhost:5173, allowed by the backend's CORS config) |
| frontend build | `cd frontend && npm run build` | Bundles the app with Vite (does not typecheck) |
| frontend preview | `cd frontend && npm run preview` | Serves the production build locally |
| backend dev | `cd backend && uvicorn app.main:app --reload` | Runs the FastAPI app with auto-reload; creates SQLite tables on startup |
| db up | `docker-compose up -d` | Starts the Postgres 16 container defined in docker-compose.yml |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `frontend/` | Vite + React 19 SPA with the approved, reviewed screens running on seeded sample data |
| `frontend/src` | Application source: main.tsx entry point, src/lib (api client, UI components, icons, navigation), styles |
| `frontend/e2e` | Playwright end-to-end specs |
| `backend/` | FastAPI service scaffold; no architecture approved yet beyond the health check |
| `backend/app` | App package: main.py (entrypoint/CORS/health route), database.py (engine/session), models.py (SQLAlchemy models, currently empty), schemas.py (Pydantic schemas, currently just a stub response), routers/ (one router per architecture component, currently empty) |
| `backend/tests` | Pytest suite (currently tests the health endpoint) |
| `.quorq/` | Platform handoff metadata (handoff.json) |
| `docker-compose.yml` | Local Postgres 16 service for development |
| `.env.example` | Template for environment variables used by the project |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend: one FastAPI router per architecture component that owns endpoints, imported into app/main.py; routes default to a typed StubResponse until implemented
- Backend: SQLAlchemy models declared in app/models.py inheriting from the shared Base in app/database.py; Pydantic request/response models live in app/schemas.py
- Backend: configuration via environment variables (DATABASE_URL, ALLOWED_ORIGINS) with sensible local defaults (SQLite, localhost:5173)
- Backend: linted/formatted with ruff (ruff.toml)
- Frontend: screens consume a shared component/icon vocabulary from src/lib/ui.tsx and src/lib/icons.tsx
- Frontend: all backend calls intended to go through the single apiFetch helper in src/lib/api.ts, which reads VITE_API_BASE_URL and VITE_API_SECRET_KEY and adds a Bearer auth header
- Frontend: linted with ESLint (eslint.config.js) and formatted with Prettier (.prettierrc)
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| backend tests | `cd backend && pytest` | Runs the pytest suite in backend/tests (pytest.ini sets pythonpath=.) |
| backend lint | `cd backend && ruff check .` | Lints the backend with ruff |
| backend format | `cd backend && ruff format .` | Formats the backend with ruff |
| frontend unit tests | `cd frontend && npm test` | Runs Vitest component tests under src/ |
| frontend typecheck | `cd frontend && npm run typecheck` | Runs tsc --noEmit (not run by npm run build) |
| frontend lint | `cd frontend && npm run lint` | Runs ESLint over the whole app; this gate must stay green |
| frontend e2e | `cd frontend && npm run test:e2e` | Runs Playwright specs in e2e/; without E2E_BASE_URL it builds/serves the frontend and boots the backend from backend/.venv automatically |
| e2e browser install | `cd frontend && npm run test:e2e:install` | Installs the Chromium browser Playwright needs |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend calls to the API fail with a CORS error | Set ALLOWED_ORIGINS (comma-separated) to the frontend's origin, or run the frontend on the default dev origins (http://localhost:5173 or http://127.0.0.1:5173) which are already allowed |
| `npm run build` succeeds but the app is broken at runtime/deploy | Run `npm run typecheck` (tsc --noEmit); build does not typecheck, so type errors like an untyped useState({}) can slip through |
| `npm run test:e2e` fails to start the backend | The Playwright config expects a Python virtualenv at backend/.venv with dependencies installed; create it and `pip install -r requirements.txt` there, or set E2E_BASE_URL to run against an already-deployed app instead |
| Backend can't find the `app` module when running pytest | Run pytest from the backend/ directory; pytest.ini sets pythonpath=. to make `import app` work from there |
| Need a persistent/shared database instead of the default SQLite file | Run `docker-compose up -d` for a local Postgres 16 instance and set DATABASE_URL accordingly; psycopg is already in requirements.txt |
<!-- sdlc:auto:end troubleshooting -->
