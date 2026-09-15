# IndiaMarket Pro — Setup Guide

Two files matter:

- **`index.html`** — the whole website, self-contained. Upload as-is.
- **`Code.gs`** — Google Apps Script that keeps your spreadsheet fed with live prices.

---

## 1. Publish the website (5 min)

1. Create a GitHub repo, e.g. `indian-stock-analysis` (must be **public** for free Pages).
2. Upload **`index.html`** to the repo root. Keep the filename exactly `index.html`.
3. Repo → **Settings → Pages** → Source: `Deploy from a branch`, Branch: `main` / `/root` → Save.
4. Wait ~2 minutes. Site is live at `https://YOURNAME.github.io/indian-stock-analysis/`.

That's it — the site works immediately using its built-in data. The steps below add live prices.

---

## 2. Connect the live spreadsheet (10 min)

Your sheet: `1eMye_WikawrpZuH_4_VklA7Gj95nKcmB_xe6GwU-gsk`

1. Go to **script.google.com** → **New project**.
2. Delete the placeholder code, paste all of **`Code.gs`**, save.
3. Confirm `SHEET_ID` at the top matches your sheet.
4. Run **`setupSheet`** once. Authorise when Google prompts (Advanced → Go to project → Allow).
5. Run **`updateAll`** once. Open the sheet — you should see rows filling in.
6. Left rail → **Triggers** (clock icon) → **Add trigger**:
   - Function: `updateAll`
   - Event source: `Time-driven`
   - Interval: **Every 5 minutes**
7. In the **spreadsheet**: **File → Share → Publish to web → Publish**. This is required — without it the website cannot read the sheet.

Reload your site. The header line should read **🟢 Live sheet connected**.

### Column contract

The website matches these header names (case-insensitive). Don't rename them:

`symbol` · `name` · `price` · `change` · `ytd` · `pe` · `dividend` · `cap` · `sector` · `updated`

Blank cells are ignored — the site keeps its built-in value for that field. So you can fill `pe` and `dividend` by hand, or from another source, without breaking anything.

### Adding more stocks

Edit the `SYMBOLS` array in `Code.gs`. Any NSE symbol works (Yahoo suffix `.NS` is added automatically).

---

## 3. Using the dashboard

**Sign in** — top right. Any username/password creates an account on first use. A seeded admin exists: `admin` / `admin123`. Or use **Continue as Guest**.

**Screener** — toggle between **Stocks** and **Mutual Funds** (same table, same features). **Top Picks** cards at the top show the three highest composite scores in the current universe. Search, sort (Composite Score / Rating / Returns / Movers), and use "+ Add & Bookmark" for any symbol not in the list. Drag the right edge of any column header to resize it.

**Score column** — a 0–100 composite blending analyst rating, YTD return, and valuation. Weights are set in Admin.

**Trend column** — a sparkline of each holding's return profile from since-inception through to today.

**⇄ Compare** — tick the ⇄ button on 2–4 rows, then click Compare for a side-by-side card table (score, price, rating, YTD, 1/3/5-year, P/E, dividend, sector).

**View** — opens the full analysis popup: price, all profit periods (1d → inception), management, growth CAGRs, growth drivers, and an inline note you can save.

**Watchlist** — create multiple named watchlists ("Bookmark1", "Long term", etc.), move stocks between them with the dropdown on each card.

**Notes** — every note you write, editable and deletable, grouped by symbol.

**Admin** (🔑 visible when signed in → ⚙️ Admin → ⚙️ Dashboard Settings):
- Which profit periods appear (1d … from-inception)
- **Composite score weights** — three sliders (rating / returns / valuation); normalised, so they needn't total 100
- Show/hide management, growth, growth drivers
- Which live parameter fills the extra table column (P/E, dividend yield, market cap)
- Define extra note columns (Risk, Target Price, …)
- Create users and set their passwords

**🔑 Password** — any signed-in user changes their own password here.

All user data (watchlists, notes, settings, accounts) is stored in the browser's local storage on that device.

---

## Troubleshooting

**Header says "Using built-in data"** — the sheet isn't published to the web. Redo step 2.7.

**Sheet stays empty** — open Apps Script → **Executions** and read the error. Usually a missing authorisation (re-run `updateAll` and accept the prompt), or Yahoo throttling (wait and retry). Run `testPublicRead` to confirm the site-facing URL returns rows.

**Site shows `{{ something }}` on screen** — you uploaded the `.dc.html` source instead of `index.html`. Upload `index.html`.

**Prices look stale** — NSE/Yahoo data is delayed ~15 min on free endpoints. The `updated` column shows the fetch time.

---

## Notes on scope

Prices, changes, YTD and market cap come from the live feed. The qualitative fields — management names, growth CAGRs, the ten growth drivers, and analyst ratings — are authored content stored in the page; no free API supplies these reliably. Edit them in the sheet or in the source, or wire a paid data provider into `Code.gs` the same way Yahoo is wired.
