# Theingabar Invoice PWA — Render deploy

Static PWA for **Theingabar Automotive Group** (သိန်းကမ္ဘာ), Aungpan.
Form -> live invoice preview -> PNG / PDF. Invoice log is a proper on-device
database (IndexedDB) with date / customer / per-item amounts / total / OK-CHECK,
CSV export + import, and a PIN lock. All data stays on the phone — no server.

Seed invoice included: **Nissan Safari, 2026-11-19, 300,000 MMK**
(120,000 + 50,000 + 130,000). KBZ Pay **09428332233, Han Min Thein** + single QR.
No logo on the invoice itself; the **HM Tech logo is the PWA icon only**.

## What's in this folder (all files go at the GitHub repo root)

| File | What it is |
|---|---|
| `index.html` | The whole app, self-contained (fonts + PNG/PDF libraries inlined) |
| `manifest.webmanifest` | PWA manifest: name **Theingabar Invoice**, standalone, navy `#0b5394` |
| `sw.js` | Service worker, cache `theingabar-v3`, caches the app for offline use |
| `icon-192.png` / `icon-512.png` | HM Tech logo app icons |
| `icon-maskable-512.png` | HM Tech logo, maskable (safe-zone padding) |
| `apple-touch-icon.png` | HM Tech logo, 180x180 for iOS |
| `render.yaml` | Render Blueprint for a Static Site (no build command, publish `.`) |
| `.gitignore` | Nothing secret is in this repo — no keys, no passwords |

## Step 1 — GitHub (Han must pick/create the repo)

1. GitHub -> **New repository** (name e.g. `theingabar-invoice`, Public or Private — either works).
2. Upload **all files in this folder to the repo root** (or `git push` them), branch **`main`**.
3. Check the repo root shows `index.html`, `manifest.webmanifest`, `sw.js`, `render.yaml`.

## Step 2 — Render (Static Site)

1. Render Dashboard -> **New -> Static Site**.
2. **Build and deploy from a Git repository** -> connect GitHub -> pick the repo above.
3. Settings (exact):
   - **Name:** `theingabar-invoice`
   - **Branch:** `main`
   - **Build Command:** *(leave empty)*
   - **Publish Directory:** `.`
4. **Create Static Site.** Wait for deploy to finish (about 1 minute, no build step).
5. URL will be like: `https://theingabar-invoice.onrender.com`
   (Render picks the exact name; if `theingabar-invoice` is taken, Render adds a suffix.)

Alternative: Render Dashboard -> **New -> Blueprint**, point it at the same repo —
`render.yaml` in the repo creates the same Static Site automatically.

## Step 3 — Install on the phone (Android / Chrome)

1. Open the Render URL in **Chrome** (not inside another app's viewer).
2. Chrome menu -> **Install app** / **Add to Home screen**.
3. It installs as **"Theingabar Invoice"** with the HM Tech logo —
   **not** Muse AI, because it now has its own domain, manifest and icons.
4. Open the installed app once online so the service worker caches it,
   then it works offline. Set the PIN from the **PIN Lock** button.

## If install still offers the wrong name

That means the browser is still on the old Muse-hosted link. Make sure you
opened the **Render** URL (`*.onrender.com`), not the `muse.ai/s/...` link,
and clear the old installed shortcut first.
