# Stitch — Projection Planner

A mobile-first web app for AV professionals to plan projector setups on-site.

## Features

- **Throw distance calculator** — enter screen width or throw distance, get lens results for every compatible optic
- **Projector & screen library** — searchable database of professional projectors (Barco, Christie, Panasonic, Epson, Sony, Digital Projection) with full lens specs
- **Inventory system** — mark the gear you own; library and calculator only show your inventory by default
- **Custom devices** — add your own projectors (with lenses) and screens
- **Unit switching** — metric (m) and imperial (ft)
- **Offline-capable** — installs as a PWA, works without internet after first load

## Stack

No build system. Each file is a self-contained HTML page.

- [Tailwind CSS](https://tailwindcss.com) via CDN
- [Material Web 3](https://github.com/material-components/material-web) components
- [Exo 2](https://fonts.google.com/specimen/Exo+2) + [Share Tech Mono](https://fonts.google.com/specimen/Share+Tech+Mono) via Google Fonts
- Vanilla JS, localStorage for persistence

## Usage

Open `index.html` directly in a browser — no server or build step needed.

> Images in the reference screens (`*/screen.png`) load from Google CDN and require an internet connection.

## Structure

```
index.html                          ← main app
manifest.json                       ← PWA manifest
sw.js                               ← service worker (offline caching)
library__projector_&_lens_details/  ← reference screen: lens detail view
projection_planner__library/        ← reference screen: projector library
projection_planner__plan_screen/    ← reference screen: plan/calculator
projection_planner__blend_screen/   ← reference screen: edge blend calculator
```

## License

MIT
