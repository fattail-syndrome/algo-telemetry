# algo-telemetry

A minimal, self-contained dashboard that visualizes the **relative performance**
of a set of systematic trading strategies. The page is a static single-page app:
it fetches live data from a read-only JSON API and re-renders in place, without
reloads.

## What it shows

- **KPI cards** — cumulative return, max drawdown, last-7-day return, annualized
  volatility, and win rate for the selected strategy.
- **Cumulative return & drawdown** — the equity curve since inception (indexed to
  0%) with a dashed zero line, over a linked drawdown panel.
- **Capital allocation** — each strategy's share of deployed capital (percentages
  only).
- **Period returns** — per-period returns at the chosen granularity (1D / 1W / 1M).
- **Correlation & statistics** — cross-strategy correlation and a risk/return table,
  shown once enough history exists to be meaningful.
- **Status mascot** — a character that reflects the selected strategy's condition.
- A live indicator and last-update time; a `STALE` badge when a series stops
  updating.

## Architecture

```
index.html   ──GET (every 30s)──▶   read-only JSON API   ◀──POST──   data pipeline
(GitHub Pages, static)                (live figures)                 (private, offline)
```

The page holds no data of its own; it polls the API and updates the DOM and the
Plotly charts (via `Plotly.react`, so there is no flicker). The API is
**read-only** from the browser's side.

## Privacy by design

Only **relative returns** and ratios are ever transmitted or displayed. There are
no absolute amounts, balances, or account details in the data or on the page — the
figures are percentage returns indexed to each strategy's start date. Any initial
capital you enter to see amounts stays in your browser and is never sent anywhere.

## Layout

```
.
├── index.html      # the static app (charts via Plotly.js CDN; fetches the API)
├── assets/         # mascot art
└── README.md
```
