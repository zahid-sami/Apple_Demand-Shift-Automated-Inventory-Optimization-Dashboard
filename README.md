# Inventory Intelligence — Automated Inventory Movement & Demand Optimization

**A working prototype that solves a real Apple retail problem: getting the right SKU to the right store before a launch weekend runs out of stock.**

> Built as an end-to-end data analytics case study — synthetic data generation → automated recommendation logic → executive-facing dashboard — using Google Apps Script and a self-contained HTML/JS analytics layer.

---

## The Problem

Every time Apple ships a new iPhone, AirPods, Watch, or iPad configuration, retail networks face the same operational headache:

- **Demand isn't even across stores.** A flagship mall location can sell through a color/storage combination in days while a smaller store sits on excess stock of the same SKU.
- **Reordering lags reality.** By the time a manual stock report flags a shortage, the launch-weekend spike has already passed and the sale is lost.
- **Nobody sees the transfer opportunity.** Store A might be overstocked on exactly the SKU Store B is about to run out of — but without a system comparing sell-through *across* stores, that stock sits idle instead of moving.
- **Discounting and stockouts happen in the same network, simultaneously** — because inventory decisions are made per-store, not network-wide.

This is the exact problem retail operations teams face during a launch cycle: **which stores need more stock, which are sitting on too much, and where should inventory physically move — automatically, not from a gut-feel weekly report.**

## The Solution

This project simulates a 10-store UAE Apple retail network (~37 SKUs across iPhone, AirPods, Apple Watch, iPad) and builds an **automated decision layer** on top of it:

1. **Data layer** — a Google Apps Script generator produces two linked datasets: a live `Inventory_Snapshot` (current stock per store × SKU) and 60 days of `Sales_Transactions` (real daily sell-through), so recommendations are grounded in actual velocity, not guesses.
2. **Recommendation engine** — every store × SKU combination is automatically classified as **Increase Stock**, **Maintain**, **Reduce Stock**, or **Move Inventory**, based on days-of-cover calculated from live sales velocity against current stock.
3. **Transfer matching** — the engine pairs overstocked store/SKU combinations with understocked ones *for the same SKU* and proposes a specific quantity to move, store to store.
4. **Executive dashboard** — a filterable, real-time interface (Date / Store / Category / Model / SKU) that surfaces the trend, the ranking, the heatmap, and the automated insights a supply-chain lead would actually act on.

This is the same logic an ops team would want running the week an iPhone launches: **spot the imbalance before it becomes a stockout, and move stock instead of waiting on a fresh order.**

---

## Live Links

| Piece | Link |
|---|---|
| 📊 Live Dashboard | `<ADD YOUR DEPLOYED DASHBOARD LINK HERE>` |
| 📝 Apps Script Project | `<ADD YOUR APPS SCRIPT PROJECT LINK HERE>` |
| 📁 Source Google Sheet (Inventory_Snapshot + Sales_Transactions) | `<ADD YOUR GOOGLE SHEET LINK HERE>` |

> **Note:** the dashboard in `/dashboard/index.html` runs fully standalone in the browser (data generation logic is mirrored in JS from the Apps Script), so it can be opened or hosted with zero setup — see [Running It](#running-it) below.

---

## Screenshots

> Replace these placeholders with real screenshots of your dashboard — this is the section that does the most work in a portfolio, so don't skip it.

| Overview | Recommendations |
|---|---|
| `docs/screenshots/overview.png` | `docs/screenshots/recommendations.png` |

| Store × SKU Heatmap | Automated Insights |
|---|---|
| `docs/screenshots/heatmap.png` | `docs/screenshots/insights.png` |

---

## How the Recommendation Logic Works

For every **Store × SKU** row:

```
avg_daily_velocity = units sold in selected window ÷ number of days
days_of_cover      = current stock ÷ avg_daily_velocity

if avg_daily_velocity == 0 and current stock > 0   → Reduce Stock (dead stock)
elif days_of_cover < 7                             → Increase Stock (understocked)
elif 7 <= days_of_cover <= 30                       → Maintain (healthy range)
elif days_of_cover > 30                             → Reduce Stock (overstocked)
```

**Move Inventory** is then layered on top: for each SKU, the engine looks across all 10 stores for a pairing where one store is flagged `Reduce Stock` (surplus, >30 days cover) and another is flagged `Increase Stock` (shortage, <7 days cover). If a pair exists, it proposes a transfer quantity — capped by what the surplus store can release above its own reorder point, and what the shortage store needs to clear its reorder threshold.

This mirrors how a real inventory planning team reasons: **cover ratio first, then look sideways across the network for a transfer before requesting fresh stock.**

---

## Dashboard Features

- **KPI strip** — Total Revenue, Units Sold, Active Stores, Active SKUs, Avg. Unit Price, each with a period-over-period delta.
- **Demand Trends** — daily / weekly / monthly toggle, units + revenue combo chart.
- **Store Performance** — ranked bar chart + table.
- **SKU & Product Analysis** — top 10 / bottom 5 SKUs, category mix, model-level revenue.
- **Store × SKU Heatmap** — top 20 SKUs by revenue across all stores, color-scaled by daily velocity.
- **Inventory Movement Recommendations** — the full classification table, filterable by recommendation type.
- **Suggested Transfers** — the automatically paired surplus → shortage transfer list.
- **High-Demand vs. Low-Demand Stores** — ranked velocity view flagging which stores should receive vs. release stock.
- **Automated Insights Panel** — plain-language findings regenerated live from whatever filter is currently active (not static commentary).
- **Global filters** — Date range, Store, Category, Model, SKU — every visual recalculates on change.

---

## Tech Stack

- **Google Apps Script** — data generation, designed to run directly inside Google Sheets (`app-script/data_generator.gs`)
- **HTML / CSS / vanilla JS** — dashboard shell and all interactivity (`dashboard/index.html`)
- **Chart.js** — trend, ranking, and distribution charts
- No backend, no build step — the dashboard is a single static file

---

## Repository Structure

```
apple-inventory-optimization/
├── README.md                     ← you are here
├── LICENSE
├── app-script/
│   └── data_generator.gs         ← generates Inventory_Snapshot + Sales_Transactions in Google Sheets
├── dashboard/
│   └── index.html                ← the full interactive dashboard (standalone)
├── data/
│   └── README.md                 ← data schema + link to the source Google Sheet
└── docs/
    └── screenshots/              ← dashboard screenshots for this README
```

---

## Running It

**Dashboard (no setup required):**
Open `dashboard/index.html` directly in a browser, or serve the repo with GitHub Pages (Settings → Pages → deploy from `/dashboard`).

**Data generator (optional — regenerate the Sheets-native version):**
1. Create a new Google Sheet
2. Extensions → Apps Script → paste in `app-script/data_generator.gs`
3. Run `generateAppleRetailData()`, authorize when prompted
4. Two sheets are created: `Inventory_Snapshot` and `Sales_Transactions`

---

## What I'd Extend Next

- Replace the synthetic 60-day window with a live Google Sheets API pull so the dashboard reflects real-time inventory instead of a generated snapshot
- Add a launch-day mode: a configurable demand multiplier to simulate the first 72 hours of a new SKU release and stress-test the recommendation thresholds
- Push transfer suggestions into an approval workflow (Slack/email notification) instead of a read-only table

---

## Author

**`<Your Name>`** — Data Analyst, [Credo Technology Services](https://www.credotechservices.com) · MBA in Business Analytics, BITS Pilani Dubai
Built as a case study for a Data Analyst interview with Viva (Landmark Group).

`<LinkedIn>` · `<Email>` · `<Portfolio>`
