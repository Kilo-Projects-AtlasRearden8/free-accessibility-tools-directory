# STATUS — Free Accessibility Tools Directory

## What was built

A free accessibility tools directory: a static HTML site (`index.html`) with client-side search and filters, plus a plain Markdown version (`tools.md`) for offline reading.

- **37 tools** covering screen readers, screen magnifiers, dictation / voice control, live captions and transcription, reading aids (incl. dyslexia-friendly fonts), local Whisper transcription, and ADHD / low-energy helpers (task, habit, focus, list, and visual organizers).
- **Built-in OS features included** (Narrator, VoiceOver, TalkBack, Orca, ChromeVox, Magnifier, Zoom, Live Captions, Voice Access, Dictation, Voice Control, Switch Control, Immersive Reader, Spoken Content, Select to Speak) alongside free third-party tools (NVDA, Orca, KMag, OpenDyslexic, Goblin.tools, Habitica, Pomofocus, Microsoft To Do, Trello, etc.).
- Grouped by **need** (Vision, Hearing, Reading & writing, Motor & dexterity, Focus & energy — 5 groups) and by **device** (Windows, macOS, Linux, iOS, Android, Web, ChromeOS — 7 groups).
- Each tool has cost, platforms, setup steps, built-in flag, tags, and an official link.
- **No affiliate links** — every link points to an official product or support page.
- **Local-first:** the site runs entirely in the browser; no server, no build step, no tracking.
- Client-side search and need/device filters (`js/app.js`, fixed so filters match the group data in `data/tools.json`).
- Published by **Asdale Dynamics, LLC** (Indiana, formed Oct 2026), credited in `README.md`, `index.html`, `tools.md`, and `LICENSE`.

## Files

- `index.html` — static site shell, search toolbar, need/device filters, results area, markdown note, footer
- `tools.md` — Markdown directory of all 37 tools, by need and by device
- `README.md` — project overview, how to run, how to add a tool, credits, license
- `LICENSE` — MIT, Copyright (c) 2026 Asdale Dynamics, LLC
- `data/tools.json` — structured source of truth for all tools and groups
- `css/style.css` — responsive styles
- `js/app.js` — loads data, renders cards, search + filters
- `scripts/verify.js` — validation checks (`npm test`)
- `package.json` — `npm test` / `npm start` scripts
- `STATUS.md` — this file

## How to run

```sh
# Option 1: open directly
open index.html   # or double-click in your file explorer

# Option 2: local server
python3 -m http.server 8000   # or: npm start
# then open http://localhost:8000
```

No install, no build step, no API keys, no secrets.

## Verification results

`npm test` — `node scripts/verify.js` — **passes**:

- `data/tools.json` is valid JSON
- All 37 tools have required fields (id, name, cost, costDetail, platforms, devices, category, need, builtIn, setup, link, tags)
- All links are valid URLs and none are affiliate links
- All group entries reference existing tools (5 need groups, 7 device groups)
- Every tool is assigned to at least one need group and one device group
- `index.html` references `css/style.css` and `js/app.js`; `js/app.js` loads `data/tools.json`
- `tools.md` mentions every tool by name

Site check: `index.html`, `data/tools.json`, and `tools.md` all return HTTP 200 when served with `python3 -m http.server` and fetched over localhost.

## Known gaps

- No automated browser tests (no headless browser available in this environment); filter/search behavior is covered manually via `scripts/verify.js` data checks.
- Data is static: new OS versions, pricing, or support URLs must be updated by hand in `data/tools.json` and `tools.md`.
- Some entries are marked beta (macOS/iOS Live Captions) or require a Microsoft/Google account for free tiers (noted in costDetail).
- OpenAI Whisper (local) requires Python and `pip` to run.
- The ChromeVox link points to the Chrome Web Store, which may change over time.
