# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the App

No build step. Open `index.html` directly in a browser, or serve locally:

```bash
python -m http.server 8080
# then open http://localhost:8080
```

A local server (rather than `file://`) is required for the service worker to register.

## Architecture

**Single-file SPA.** All application logic lives in `index.html` — HTML structure, CSS styles, projector/screen database, and vanilla JS are all inline in one file (~1500+ lines). There is no framework, bundler, or build system.

**External dependencies via CDN only:**
- Tailwind CSS (utility classes)
- Material Web 3 (`@material/web`) — used for `md-tabs`, `md-filter-chip`, `md-chip-set`, `md-secondary-tab`
- Google Fonts: Exo 2 (UI), Share Tech Mono (numeric readouts)
- Material Icons Round

**State management:** A single `state` object holds runtime state. All persistence is via `localStorage` under `stitch-*` keys:
- `stitch-unit` — metric/imperial toggle
- `stitch-custom` — user-added projectors
- `stitch-screens` — user-added screens
- `stitch-inv-proj` / `stitch-inv-scr` / `stitch-inv-lens` — owned inventory sets
- `stitch-show-all` — library filter toggle

**Data:** Built-in projector database (`PROJECTORS` array) and screen database (`SCREENS` array) are defined as JS constants in `index.html`. Custom devices are merged in via `allProjectors()` / `allScreens()`.

**Navigation:** Tab-based UI (`switchTab(name)`). Bottom nav switches between: Library (projectors + screens sub-tabs), Calculator, and Settings. Modals are bottom sheets toggled via `openModal(id)` / `closeModal(id)`.

**PWA:** `manifest.json` + `sw.js` enable installation and offline use. The service worker uses cache-first for same-origin assets and network-first for CDN resources.

## Reference Screens

The `projection_planner__*/` and `library__*/` directories each contain:
- `code.html` — standalone reference/prototype for that view
- `screen.png` — design reference image (loads from Google CDN)

These are design references only and not part of the main app.

## Key Conventions

- CSS custom properties (`--primary`, `--bg`, `--s1`–`--s3`, etc.) define the dark amber theme. Primary accent is `#f5a623`.
- Numeric readouts use the `.readout` class (Share Tech Mono font).
- Unit conversion: `toDisplay(meters)` / `fromDisplay(displayValue)` handle m↔ft.
- Inventory keys use `projKey(p)`, `scrKey(s)`, `lensKey(p,l)` — string identifiers used in the inventory arrays.
- Animation: cards use CSS `fadeUp` keyframes; reduced-motion media query disables all transitions.
