# VFX Bid Sheet

A single-file, offline-capable bidding tool for VFX assets and shots. No build step, no backend, no dependencies to install.

## Deploy to GitHub Pages

1. Create a new repository (private is fine for the code, but note Pages from a private repo requires a paid plan — see below).
2. Upload `index.html` to the root of the repo. The web UI works: **Add file → Upload files**.
3. **Settings → Pages → Source:** `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. Wait ~60 seconds. The site is live at `https://<username>.github.io/<repo>/`.

That's the whole deployment. Any future edit is a commit to `index.html`.

### Public vs private

GitHub Pages only serves from private repos on paid plans. Two options:

- **Public repo, private bids.** The tool contains no client data, so publishing it is harmless. Keep exported bid JSONs in a separate private repo or a Drive folder.
- **Paid plan, private repo.** Everything in one place.

Do not commit bid JSONs to a public repo — they contain rates and client figures.

## Running locally

Open `index.html` in any browser. It works from the filesystem — no server needed.

## Where data is stored

Bids are saved to **IndexedDB** in the browser, under the origin the page is served from. Practical capacity is hundreds of megabytes, which matters because thumbnails are stored inline as compressed data URLs.

Consequences worth knowing:

- Storage is **per-browser and per-device**. A bid saved on your laptop will not appear on your phone.
- Storage is **per-origin**. Bids saved from `file://` are separate from bids saved from the Pages URL.
- Clearing browsing data deletes saved bids.

**Exported JSON is the real backup.** Use *File → Backup (JSON)* regularly, especially before switching devices or sharing.

## Exports

- **Client bid (HTML)** — clean, light, print-to-PDF summary. Hides rates, complexity multipliers and per-discipline breakdown; shows thumbnails, durations, days, costs, overheads and assumptions.
- **Working sheet (CSV)** — full internal detail, opens in Excel or Google Sheets.
- **Backup (JSON)** — complete state including thumbnails. Self-contained and shareable.

## Editing

The app is plain JSX compiled in the browser by Babel. Open `index.html` in a text editor, find the `<script type="text/babel">` block, edit, save, commit. No toolchain.

The trade-off is a one-off ~1MB Babel download on first visit (cached thereafter). If that becomes annoying, the JSX can be precompiled with esbuild and the Babel script tag dropped.
