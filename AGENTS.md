# AGENTS.md

## Project Overview
Fretta is a single-file static HTML logistics app (Portuguese, pt-BR). No build step, no backend, no package manager.

## Architecture
- `index.html` — the entire app: HTML, CSS, and JavaScript inline.
- Uses CDN-hosted SDKs: Supabase (auth + DB), MercadoPago (Pix payments), QRCode.js.
- Supabase URL and anon key are hardcoded client-side (public by design). Falls back to local mode if Supabase is unreachable.
- MercadoPago uses a test key (`APP_USR-...`).

## Running in the Sandbox
- `docker compose -f docker-compose.base44.yml up -d` — serves `index.html` via nginx:alpine on port 3000.
- No environment variables or secrets required to boot. The app works in local mode without Supabase.
- Healthcheck: `wget --spider http://localhost:80/` inside the container.

## Notes
- This is a static site; edits to `index.html` require a `reload_preview` call (nginx serves the bind-mounted file, but the preview iframe needs a forced refresh).
- No tests configured.
