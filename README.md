# WebOS
# Webtop
# The Vault

Webtop is a full-screen, macOS-inspired desktop simulator built with Vite, React, Zustand, react-rnd, framer-motion, cmdk, and Supabase.
The Vault is a modern dark-theme MVP for a password-protected unblocked games platform. It is built with Vite, React, and TypeScript and is ready to upload to Render as a static site.

## Features
## MVP features

- Full-screen gradient desktop with no document scrolling
- Translucent menu bar with focused app title and live clock
- macOS-style dock with hover magnification and open-app dots
- Draggable, resizable, minimizable, maximizable windows
- Cmd/Ctrl+K Spotlight palette for apps and files
- Supabase email/password auth with local demo fallback
- Finder, Notes, Editor, and Settings apps
- User preferences for wallpaper and light/dark theme
- Debounced note and window-session persistence
- Password gate for the full site with a session unlock flow.
- Site and admin passwords are compared against SHA-256 hashes supplied by environment variables instead of plaintext constants.
- Failed login tracking locks the local device for 72 hours after 3 consecutive failures and exposes lockouts to administrators.
- Searchable 60+ game library including Sandboxels and Geometry Dash.
- Category filters, featured games, favorites, and recently played games.
- 55GMS proxy workspace with URL input, loading state, error fallback guidance, and persisted sessions.
- Secure admin dashboard for maintenance mode, lockout management, game CRUD, featured games, and site settings.
- Responsive dark UI with sidebar navigation, cards, smooth hover transitions, and fast-loading lazy thumbnails.

## Local development

```bash
npm install
npm run dev
```

For Supabase-backed auth/data, copy `.env.example` to `.env` and fill in your project values.
## Render deployment

## Supabase setup
This repository includes `render.yaml`, so it can be deployed through Render Blueprints or as a manually configured Static Site.

Run `src/schema.sql` in your Supabase SQL editor before using the hosted data mode.
### Blueprint deploy

## Render deploy
1. Push the repository to GitHub or GitLab.
2. In Render, choose **New +** → **Blueprint**.
3. Select this repository.
4. Add the required secret environment variables when Render prompts for them:
   - `VITE_SITE_PASSWORD_HASH`
   - `VITE_ADMIN_PASSWORD_HASH`
5. Deploy. Render will run `npm install && npm run build` and publish the `dist` directory.

Use a Render Static Site:
### Manual Static Site deploy

- Build command: `npm install && npm run build`
- Publish directory: `dist`
- Environment variables: `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`
Use these Render settings:

- **Runtime:** Static Site
- **Build Command:** `npm install && npm run build`
- **Publish Directory:** `dist`
- **Rewrite Rule:** `/*` → `/index.html`
- **Node Version:** `20`

## Password hashes

Set these Vite environment variables before building:

- `VITE_SITE_PASSWORD_HASH`: SHA-256 hash of the visitor site password.
- `VITE_ADMIN_PASSWORD_HASH`: SHA-256 hash of the administrator password.

Generate hashes locally with:

```bash
printf 'your-password' | sha256sum
```

Demo fallbacks are available for local testing only:

- Site password: `123456`
- Admin password: `vault-admin`

For a production deployment, pair this MVP with HTTPS, a server-side database, HttpOnly secure cookies, CSRF tokens for mutations, and a server-side proxy service for 55GMS traffic.

## Build

```bash
npm run build
```
