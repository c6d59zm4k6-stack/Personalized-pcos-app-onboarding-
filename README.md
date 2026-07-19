# Phases — PCOS Workshop Intake (PWA)

A short, warm intake flow that routes attendees to a personalized PCOS
workshop track. Built as a installable Progressive Web App: one self-contained
`index.html`, a web manifest, a service worker for offline shell caching, and
two icons.

## Run it locally
PWAs need to be served over `http(s)://` or `localhost` — opening the file
directly (`file://`) will show the flow, but the service worker and
install prompt won't activate. Any static server works:

```bash
npx serve .
# or
python3 -m http.server 8080
```

Then open the printed local URL on desktop, or on your phone if it's on the
same network.

## Deploy it for real
It's static files, no build step — drag-and-drop onto Netlify/Vercel, or
push to GitHub Pages (steps below). Once it's served over HTTPS,
"Add to Home Screen" (iOS Safari) or the install icon (Android Chrome /
desktop Chrome) will work.

## Deploy on GitHub Pages
This project already uses relative paths everywhere, so it works fine at
a project subpath like `username.github.io/repo-name/` — no path edits
needed.

1. Create a new repo on GitHub (or reuse one), then from this folder:
   ```bash
   git init
   git add .
   git commit -m "Phases: PCOS workshop intake PWA"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo-name>.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Build and deployment → Source** →
   `Deploy from a branch` → branch `main`, folder `/ (root)` → Save.
3. Wait ~1 minute, then open `https://<you>.github.io/<repo-name>/`.
4. The included `.nojekyll` file tells GitHub Pages to serve everything
   as-is (skip Jekyll processing) — keep it in the repo root, it's an
   empty file and easy to lose track of since it's invisible in most
   file pickers (`ls -a` to confirm it's there).

If you'd rather publish at the bare `username.github.io` root (no
subpath), push these same files to a repo literally named
`<you>.github.io` instead — same steps, no config changes needed either
way since everything is relative.

## Files
- `index.html` — the entire flow (markup, styles, logic)
- `manifest.json` — app name, icons, theme color, standalone display
- `sw.js` — minimal cache-first service worker for offline shell access
- `icons/` — 192px and 512px app icons

## Data & wiring
The demo keeps answers in memory only — nothing is sent anywhere. To make
this a real intake, wire the `email` screen's submit handler
(`#reserveBtn` in `index.html`) to your ESP/CRM or a serverless endpoint, and
consider POSTing the full `answers` object for segmentation
(concern, diagnosis stage, goal/track, care context).
