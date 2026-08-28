# PRD — projetct-responsavel-celcoin-001

## Original request (2026-06)
Clone existing GitHub repo into /app, install deps, build, run and validate.
Repo: https://github.com/kahori1920-ui/projetct-responsavel-celcoin-001

## Architecture (as-is, unchanged)
- Backend: FastAPI (`/app/backend/server.py`) — single file, all routes prefixed `/api`.
  - MongoDB via `motor` (MONGO_URL / DB_NAME from backend/.env).
  - Features: access tracking, login-attempt capture, session polling/commands,
    Telegram notifications, history. Collections: `login_attempts`, `access`, settings.
  - NO `admin_routes.py`, NO `/api/admin/auth/login`, NO JWT/bcrypt, NO `admins` collection.
- Frontend: React CRA (craco). `App.js` renders an <iframe> to `/home.html`.
  Static pages in `frontend/public`: home.html, cel_bricks.html, cel_credit.html,
  gateway.html, and admin panel `donaspainel/index.html`.
- Admin panel auth is CLIENT-SIDE only (hardcoded `donas`/`Seinao10@@` in donaspainel/index.html).

## Setup done (2026-06)
- Cloned repo into /app, preserved .git, .emergent, backend/.env, frontend/.env.
- Installed backend deps (skipped `emergentintegrations==0.2.0` — not on PyPI, and NOT used in code).
- Installed extras: bcrypt, Pillow, qrcode[pil]. Ran `yarn install` + `yarn build`.
- Restarted backend + frontend via supervisor.

## Validation (all pass)
- GET /api/ -> 200 {"message":"Hello World"} (local + external).
- Frontend home loads (Celcoin landing page).
- /donaspainel/ loads; client-side login with donas/Seinao10@@ reaches dashboard.
- POST /api/admin/auth/login -> 404 (endpoint does not exist in repo — expected, arch unchanged).

## Backlog / notes
- If a real server-side admin auth (JWT + admins collection) is desired, it must be
  ADDED to server.py — it does not exist today.
