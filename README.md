# launchwingman.com — Wingman download landing page

The public site at **https://launchwingman.com**, served by **GitHub Pages** (Cloudflare-fronted). Its only job
is to let a visitor download the latest **Wingman for Windows** installer.

## How it works
1. On load, `index.html` fetches the update manifest **https://software.launchwingman.com/latest.json** — the same
   manifest the in-app auto-updater reads, so the site and the app always agree on the current release (single
   source of truth).
2. It shows the latest version + date and enables the **"Download Wingman for Windows here"** button, whose href is
   the manifest's `installerUrl` (the signed `.exe` hosted on the public `wifi-consultant/wingman-downloads` repo).

## ⛔ BUTTON-ONLY — do NOT auto-download
The download must start **only when the visitor clicks the button — NEVER automatically on page load.** Do **not**
re-add an auto-navigate (`setTimeout(function(){ window.location.href = installerUrl }, …)`) or any other code that
begins a download without a click. Simply visiting the page must not trigger a download. (An earlier version
auto-started the download; that was removed on 2026-09-28 — keep it button-only.)

## Files
- `index.html` — the page (fetch manifest → show version → download **button**).
- `404.html` — **kept byte-identical to `index.html`** so any path under the domain renders the same page.
- `CNAME` — `launchwingman.com`.
- `.nojekyll` — serve files as-is (no Jekyll processing).

## Updating
Edit `index.html`, mirror the **exact same change into `404.html`** (keep the two identical), and push to `main`.
GitHub Pages redeploys in ~30–90 s.
