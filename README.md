# algo-telemetry

A minimal, static dashboard that visualizes the **relative performance** of a set
of systematic trading strategies. It is a self-contained page: open `index.html`
(or the hosted site) and switch between the combined portfolio and each individual
strategy.

## What it shows

- **KPI cards** — cumulative return, maximum drawdown, and last-7-day return for
  the selected strategy.
- **Cumulative return** — the equity curve since inception, indexed to 0%.
- **Drawdown** — the decline from the running peak of cumulative return.
- **Descriptions** — a short summary of each strategy's style.
- **Freshness** — the last update time and a `STALE` badge when a series has not
  been refreshed recently.

## Data

The page is driven entirely by the CSV files in `data/`. Each file is one strategy
and contains only two columns:

| column | type | description |
|--------|------|-------------|
| `date` | `YYYY-MM-DD` | one row per day, ascending |
| `ret`  | float | daily simple return as a decimal, net of costs (`0.0031` = +0.31%) |

Cumulative return is `∏(1 + ret) − 1`; drawdown is `equity / cummax − 1`.

## Privacy by design

Only **relative returns** are ever stored or displayed. There are no absolute
amounts, balances, or account details anywhere in the data or the page — the
figures are purely percentage returns indexed to each strategy's start date.

## Layout

```
.
├── index.html      # the dashboard (self-contained; charts via Plotly.js CDN)
├── data/           # one <strategy>.csv per strategy (date, ret)
└── README.md
```
