# Trader Desk — benchmark prompt (backend + frontend)

Paste into **Cursor Agent**, Cline, or any orchestrator window.

---

You are building a **Trader Desk** benchmark deliverable.

Your creative angle: interpret “desk” as a **multi-panel trading floor** — watchlist, main chart, order flow / book or tape, status bar; **asymmetric layout**, not a symmetric card grid.

Deliver a complete **Trader Desk**: **Python FastAPI backend** + **separate frontend** — not a plan-only reply, not a fake delivery report.

All files under `trader-desk/`.

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

Include **at least 3 functional regions** on screen (e.g. header + main chart + side panel + footer tape). One flat grid of identical widgets is discouraged.

## Architecture (mandatory)

### Backend — `trader-desk/backend/`

- **Python + FastAPI** (prefer FastAPI over Flask).
- **Fetches real market data** from public APIs (Yahoo, Coinbase, Binance, etc.). Test with `curl` first.
- **No fake/hardcoded prices** in API responses (except clearly labeled demo fallback if upstream is down).
- Expose REST JSON, minimum:
  - `GET /health`
  - `GET /api/symbols` — tracked symbols
  - `GET /api/quotes` — current quotes for all 8 symbols
  - `GET /api/quotes/{symbol}` — one symbol detail (price, change, intraday/OHLC if available)
  - Add more routes if your UI needs them (candles, order book, tape, etc.)
- **CORS enabled** for the frontend origin.
- `trader-desk/backend/data_sources.json` — every upstream URL you call.
- `trader-desk/backend/requirements.txt`

Backend owns API keys, proxies, rate limits, and upstream retries. **The browser must NOT call Yahoo/Binance/Coinbase directly.**

### Frontend — `trader-desk/frontend/`

- Separate app: **HTML + CSS + JS** (no build step) **or** React + Vite (include `package.json`; must run with `npm install && npm run dev`).
- **All data via your backend only** (`fetch('http://localhost:8000/api/...')` or relative `/api` behind a proxy).
- **No hardcoded quote arrays** in frontend source.
- Dark theme (interpret the palette yourself).
- All text and symbols **≥ 20px**.
- Show these symbols with live or delayed real data: **NVDA, AAPL, TSLA, MSFT, BTC-USD, ETH-USD, SOXL, SPY**.
- Loading and error states when the API fails.
- 2D only. Canvas/SVG charts OK. No WebGL.

## Rules

- Create **real files on disk**. No fake delivery reports, no file tree without files.
- If you cannot write files, say so and stop.
- Plan first (concept + APIs + folder layout), then implement **backend**, then **frontend**, then README with run commands.

## Step 0 — Plan first

Reply with **### Planned actions**:

1. **Research** — public APIs, `curl` tests, CORS/proxy strategy on the backend.
2. **Architecture** — `trader-desk/backend/`, `trader-desk/frontend/`, API contract (JSON examples).
3. **Your chosen UI concept** — name it; describe layout regions and why they fit a trading floor.
4. **Acceptance** checklist.

Then execute.

## Deliverables

```
trader-desk/
  backend/
    main.py              (or app package)
    requirements.txt
    data_sources.json
  frontend/
    index.html           (+ style.css, app.js — or React src/)
  README.md              — concept, APIs, how to start backend + frontend
```

**README must include:**

```bash
# terminal 1 — backend
cd trader-desk/backend
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 8000

# terminal 2 — frontend
cd trader-desk/frontend
# static: python3 -m http.server 8080
# or React: npm install && npm run dev
```

Open the frontend URL in a browser; quotes must load from your API.

## Acceptance

- [ ] Backend starts; `/health` returns OK
- [ ] `/api/quotes` returns real data for all 8 symbols (or clear per-symbol errors)
- [ ] Frontend renders without build errors (or `npm run dev` works)
- [ ] Frontend shows quotes from backend only
- [ ] `data_sources.json` lists upstream APIs
- [ ] README run instructions work
- [ ] UI has ≥ 3 functional regions and a distinctive layout (not a generic 8-card grid)
