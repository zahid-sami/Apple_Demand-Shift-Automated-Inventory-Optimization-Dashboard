<div align="center">

<img src="https://www.shutterstock.com/search/iphone-logo"/>

# Apple Restock Radar
### Automated Inventory Movement Dashboard

**Stops stockouts before they happen — and tells you exactly which store to move stock from.**

![Google Apps Script](https://img.shields.io/badge/Google_Apps_Script-4285F4?style=flat-square&logo=google&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white)
![HTML/JS](https://img.shields.io/badge/HTML%2FJS-E34F26?style=flat-square&logo=html5&logoColor=white)

[**🔴 Live Dashboard**](https://script.google.com/macros/s/AKfycbw_6I2KFcDJWLebVQY54prE55m8CL6AKuGK4Pduq0OnEWLNeAya24GZstodqkY9osaVLA/exec) · [**Apps Script**](https://script.google.com/u/0/home/projects/1jjbVTxflR9WU0GqQWTYtqucqNQcBndL8xK-5Ad3WNM7107IeV6WWsTsD/edit) · [**Google Sheet**](https://docs.google.com/spreadsheets/d/1XFfHsOKQQAmvy0YUpIQ3s2CsK-FwGGzG3GloysIcE0c/edit?gid=1731239860#gid=1731239860)

</div>

---

## 🔴 The Problem

When a new iPhone / AirPods / Watch / iPad drops, retail networks lose money in two places at once:

- One store **sells out** in days and turns customers away
- Another store, same SKU, sits on **excess stock** nobody's buying
- No one's comparing the two — so the transfer that would fix both never happens

## 🟢 The Solution

**RestockRadar** tracks sell-through vs. stock across 10 stores × 37 SKUs and auto-flags the fix:

| Signal | Action |
|---|---|
| < 7 days of stock left | 🔺 **Increase Stock** |
| 7–30 days of stock | ✅ **Maintain** |
| 30+ days, slow mover | 🔻 **Reduce Stock** |
| Overstocked here, short there | 🔁 **Move Inventory** — with store + quantity |

Filter by store, category, model, or date — every chart and recommendation updates live.

## 📸 Dashboard

<div align="center">
<img src="" width="90%" alt="C:\Users\zahid\OneDrive\Documents\Pictures\Screenshots\Screenshot 2026-08-14 010710.png"/>
<br><br>
<img src="" width="90%" alt="add recommendations screenshot URL here"/>
</div>

## ⚙️ How It Works

```
avg daily sales → days of stock cover → auto-classify → match surplus store to shortage store
```

1. **Apps Script** generates live inventory + 60 days of sales in Google Sheets
2. **Dashboard** classifies every store × SKU and recommends transfers
3. **Insights panel** regenerates plain-language findings on every filter change

## 🔗 Links

| | |
|---|---|
| Automated Live Dashboard | https://script.google.com/macros/s/AKfycbw_6I2KFcDJWLebVQY54prE55m8CL6AKuGK4Pduq0OnEWLNeAya24GZstodqkY9osaVLA/exec |
| Apps Script | https://script.google.com/u/0/home/projects/1jjbVTxflR9WU0GqQWTYtqucqNQcBndL8xK-5Ad3WNM7107IeV6WWsTsD/edit |
| Google Sheet | https://docs.google.com/spreadsheets/d/1XFfHsOKQQAmvy0YUpIQ3s2CsK-FwGGzG3GloysIcE0c/edit?usp=sharing |

---
<div align="center"><sub>Built by <b>&lt;Your Name&gt;</b> — Data Analyst · Case study for a Data Analyst interview with Landmark Group</sub></div>
