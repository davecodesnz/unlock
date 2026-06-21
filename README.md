# Unlock

A daily jobs + screen-time app for kids. Jobs must be done (and a timed times-tables test passed) before screen time unlocks. A parent enters a PIN to confirm.

**Live demo:** https://unlock-production-6014.up.railway.app

## What it does
- Three phases a day — **Morning**, **After school**, **After dinner** — auto-selected by time of day
- Each phase has a checklist of jobs plus a **times tables test** (8 questions, need 5 correct, 3-minute timer)
- Day-specific jobs appear automatically (e.g. bins out on Monday, Number Works homework Mon/Wed)
- When all jobs + the test are done, a parent enters the code (**1980**) to unlock screens
- Progress saves to the device and resets at midnight
- Times-tables questions (2–12) are randomised and avoid recent repeats

## Run it locally
Requires [Node.js](https://nodejs.org) 18+.

```bash
npm start
# open http://localhost:3000
```

The whole app is a single file — `index.html`. Edit it and refresh; no build step.

## Make it your own
- **Jobs / phases / times:** edit the `buildPhases()` function in `index.html`
- **Parent code:** search for `'1980'` in `index.html`
- **Test difficulty:** see `genQs()` (the `rnd(2,12)` range) and the pass mark (`tt.correct >= 5`)
- **Colours / fonts:** the `:root` CSS variables at the top of the `<style>` block

## Deploy your own copy (Railway)
1. Fork this repo
2. Create a [Railway](https://railway.com) account
3. New Project → Deploy from GitHub repo → pick your fork
4. Railway auto-detects Node and runs `npm start`; add a public domain under the service's Settings → Networking

Every push to `main` then auto-deploys.

## Files
| File | Purpose |
|------|---------|
| `index.html` | The entire app (UI + logic) |
| `favicon.svg` | Phone-in-jail icon |
| `server.js` | Tiny zero-dependency static file server |
| `package.json` | `npm start` entry point |
