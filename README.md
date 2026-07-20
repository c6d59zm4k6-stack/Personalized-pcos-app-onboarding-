# Phases — PWA

A small, installable web app (works offline once loaded, can be added to a phone's home screen).

## Files
- `index.html` — the app
- `manifest.json` — PWA metadata (name, icons, colors)
- `sw.js` — service worker (caches the app so it works offline)
- `icons/` — app icons
- `.nojekyll` — tells GitHub Pages to serve files as-is

## Deploy on GitHub Pages

1. Create a new repository on GitHub (public or private both work).
2. Upload all the files in this folder to the repo, keeping the `icons/` folder intact.
   - Easiest: on the repo page, "Add file" → "Upload files" → drag in everything, including `.nojekyll` (GitHub may hide it — if you don't see it in the upload list, use `git` instead, see below).
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to "Deploy from a branch," branch `main`, folder `/ (root)`. Save.
5. Wait about a minute, then visit `https://<your-username>.github.io/<repo-name>/`.

### Using git instead of drag-and-drop (recommended — handles the .nojekyll file reliably)
```
git init
git add -A
git commit -m "Add Phases PWA"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```
Then do steps 3–5 above.

## Installing it as an app
- **iPhone (Safari):** open the URL → Share → "Add to Home Screen."
- **Android (Chrome):** open the URL → ⋮ menu → "Install app" (or "Add to Home screen").

## Notes
- Everything runs client-side — no backend, no data leaves the device except the optional email field, which currently isn't sent anywhere (there's no server). If you want submissions to go somewhere, you'll need to add a form endpoint (e.g. Formspree, a Google Form, or your own backend) and wire up the "Reserve my spot" button in `index.html`.
- If you rename the repo or move the site under a different path, the relative paths in `manifest.json`, `sw.js`, and `index.html` will still work — nothing is hardcoded to a specific URL.
