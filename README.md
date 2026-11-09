# launchwingman.com — Wingman download landing page

The public site at **https://launchwingman.com**, served by **GitHub Pages** (Cloudflare-fronted). Its only job
is to let a visitor download the latest **Wingman for Windows** installer, the
**WingmanOne** image (when published) and the **Wingman Eagleview** installer.

## How it works
1. On load, `index.html` fetches the update manifest **https://software.launchwingman.com/latest.json** — the same
   manifest the in-app auto-updater reads, so the site and the app always agree on the current release (single
   source of truth).
2. It shows the latest version + date and enables the **"Download Wingman for Windows here"** button, whose href is
   the manifest's `installerUrl` (the signed `.exe` hosted on the public `wifi-consultant/wingman-downloads` repo).

## Card icons = the family marks (2026-11-09)
The three download cards draw the real product marks with the page's own W generator (`wBlocks` / `tileMark` /
`oneMark` in `index.html`): **Wingman** = the app icon (white rounded tile, the tetris W); **Wingman Eagleview** =
the same tile and W in its cool-green palette with the warm block above the W's centre as a map pin; **WingmanOne**
= the W inside the handheld outline with the word "One". Same `W_D` bitmap and block style as the badge, favicon and
wordmark; the Wingman app icon (`wingman` repo `scripts/gen-icon.cjs`) and Eagleview's (`eagleview` repo
`tools/make_icons.py`) use the same tile numbers (5.5 % margin, 26 % radius, `#e7e5f1` border, W at 60 %).

## Wingman Eagleview card (added 2026-11-09)
The third card reads Eagleview's OWN manifest, **https://software.launchwingman.com/eagleview/latest.json**
(the root `latest.json` is the Windows Wingman app's; Wingman One will get its own folder), and sets the
button's href to its `installerUrl` (the `Eagleview-Setup-<version>.exe` Release asset on the public
`wifi-consultant/eagleview-downloads` repo). It is never the "For your device" pick and always sits third.
Same button-only rule as below. The card uses this page's styling only; the Eagleview app itself carries
no Wingman branding yet.

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
