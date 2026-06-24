# Trader Desk — benchmark prompt

You are building a Trader Desk benchmark deliverable. Your creative angle: interpret “desk” as a multi-panel trading floor — watchlist, main chart, order flow / book or tape, status bar; asymmetric layout, not a symmetric card grid.

Build a Trader Desk — a single-screen market workspace — as real files in `trader-desk/`.

## Creative mandate (read this first)

You decide everything about the product. We are comparing how different models think a trader desk should look and work — not whether everyone can copy the same card grid.

Before writing code, pick one clear concept and name it in your plan, for example:

- watchlist + intraday chart + order book
- heatmap / sector matrix
- scrolling ticker tape + detail pane
- table-first blotter with sortable columns
- single-symbol focus with multi-timeframe charts
- risk dashboard (exposure, PnL, alerts) — not just quotes

Do not default to “8 equal cards in a responsive grid” unless you explicitly choose that layout and explain why it fits your concept.

Aim for a distinctive UI: typography, color system, panel layout, and information hierarchy should feel like your design — not a generic dark dashboard template.

Include at least 3 functional regions on screen (e.g. header + main chart + side panel + footer tape). One flat grid of identical widgets is discouraged.

## Rules

- Create real files on disk. No fake delivery reports.
- HTML + CSS + JS only — `index.html` plus optional `style.css`, `app.js`.
- No React, Vite, npm, backend, FastAPI.
- Must open in a browser with no build step.
- Find real market data yourself — search public APIs, test with curl, load via `fetch()` in the browser. No hardcoded fake prices.
- Write `trader-desk/data-sources.json` listing every API URL you use.
- 2D only. Canvas/SVG charts OK. No WebGL.

## UI constraints (minimal)

- Dark theme (interpret the palette yourself)
- All text and symbols ≥ 20px
- Show these symbols somewhere with live or delayed real data: NVDA, AAPL, TSLA, MSFT, BTC-USD, ETH-USD, SOXL, SPY

Layout, components, charts, refresh UX, error handling — entirely your call.

## Deliverables

- `trader-desk/index.html`
- `trader-desk/data-sources.json`
- `trader-desk/README.md` — concept, APIs, how to open

Plan first: your chosen concept + APIs (1 short paragraph each), then build all files.
