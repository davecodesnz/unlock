# CLAUDE.md — project context for Claude Code

## What this is
**Unlock** — a daily jobs + screen-time app for a 12-year-old. Jobs must be completed and a timed times-tables test passed before screen time unlocks; a parent enters a PIN to confirm. Single-page app, no framework, no build step.

## Architecture (read this first)
- **The entire app is `index.html`** — all HTML, CSS, and JS in one file. There is no framework, bundler, or build step. Edit and refresh.
- `server.js` is a tiny zero-dependency Node static server (reads Railway's `$PORT`). Only used for serving in production.
- `package.json` → `npm start` runs the server. `favicon.svg` is a phone-behind-bars icon.
- State persists in `localStorage` under the key `unlock_v11`; it resets daily (keyed on the date string) and keeps a rolling history of recent quiz questions to avoid repeats.

## Key concepts in index.html
- `buildPhases()` returns the three daily phases (`morning`, `afterschool`, `evening`), each with its job list. Day-specific jobs are added conditionally (e.g. Monday bins, Mon/Wed Number Works homework). **Edit jobs here.**
- Phase is auto-selected by time of day in `getTimePhase()`.
- `genQs()` generates the times-tables questions (2–12), unique within a session and avoiding the last 24 seen. Pass mark is `tt.correct >= 5` of 8; timer is 180s in `startTT()`.
- Parent PIN is the literal `'1980'` in `press()`. (Consider moving to config if making the repo public.)
- Screens are sibling `.screen` divs toggled by `showScreen(id)`. Bottom nav = `navTo()`.

## Conventions
- Match the existing style: vanilla JS, terse helper functions, Material Symbols icons, the `--*` CSS custom properties at the top of `<style>` for all colours.
- No dependencies. Keep it a single self-contained `index.html` unless there's a strong reason not to.
- Two font families only (Plus Jakarta Sans + Material Symbols), both from Google Fonts.

## Run locally
```bash
npm start   # http://localhost:3000
```

## Deploy (Railway, auto-deploy from GitHub)
- Fork the repo, create a Railway project from your fork. Railway auto-detects Node and runs `npm start`.
- Add a public domain under the service's Settings → Networking.
- Every push to `main` auto-deploys.
