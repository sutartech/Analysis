# Indian Stock & MF Analysis Website - Complete Setup Guide

## 🚀 Quick Start (15 mins)

### Step 1: Create GitHub Repository
1. Go to **github.com** → Sign in
2. Click **+ → New repository**
3. Name: `indian-stock-analysis`
4. Make it **Public**
5. Click **Create repository**

### Step 2: Set Up Google Apps Script
1. Go to **script.google.com**
2. Click **+ New project**
3. Name it: `Stock Data Fetcher`
4. Copy entire `Code.gs` file content into the editor
5. Replace `YOUR_GITHUB_TOKEN_HERE` with your GitHub token:
   - Go to github.com → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click **Generate new token (classic)**
   - Select: `repo` (full control of private repositories)
   - Copy token & paste in Code.gs
6. Replace `username/indian-stock-analysis` with your repo name
7. Click **Deploy → New deployment → Web app**
8. Execute as: Your account
9. Allow access: Anyone
10. Copy deployment URL (save for later)

### Step 3: Create GitHub Folders & Files
1. In your repo, click **Add file → Create new file**
2. Path: `data/stocks.json`
3. Paste:
```json
[
  {
    "symbol": "RELIANCE",
    "name": "Reliance Industries",
    "price": 2950,
    "change": 3.1,
    "rating": 5,
    "sentiment": "bullish",
    "ytd": 22.5,
    "pe": 20.5,
    "dividend": 0.7,
    "cap": 3820000,
    "sector": "Energy"
  }
]
```
4. Click **Commit changes**

5. Create `data/mfs.json`:
```json
[
  {
    "name": "HDFC Top 100 Fund",
    "returns1y": 18.5,
    "returns3y": 12.3,
    "rating": 5,
    "aum": "₹45,000 Cr",
    "category": "Large Cap"
  }
]
```

6. Create `index.html` → Paste the full DC HTML from the website file

### Step 4: Enable GitHub Pages
1. Go to repo → **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** (or master)
4. Folder: **root**
5. Click **Save**
6. Wait 2-3 mins → Your site is live at: `https://yourusername.github.io/indian-stock-analysis`

### Step 5: Set Up Automated Updates
1. Go back to **Google Apps Script** project
2. Click **Triggers** (clock icon on left)
3. Click **+ Create a new trigger**
4. Configure:
   - Function: `fetchAndUpdateStocks`
   - Deployment: `Head`
   - Event type: `Time-driven`
   - Type: `Minutes timer`
   - Frequency: `Every 5 minutes`
5. Click **Save**

Now your data updates automatically every 5 minutes! 🎉

---

## 📊 Data Sources

### Primary APIs (Free Tiers)
- **NSE India API** – https://www.nseindia.com/api
  - Stock prices, volumes, change %
  - No auth required
  
- **yfinance** – https://rapidapi.com/spartan737/api/yfinance-api
  - Historical prices, PE ratios, dividends
  - Free tier: 500 calls/month

- **Alpha Vantage** – https://www.alphavantage.co
  - Intraday, historical data
  - Free tier: 5 calls/min, 500/day

- **Rapid API** – Multiple stock market APIs
  - Indian stock data, MF returns
  - Free tier varies by API

### Recommended Setup
For 10 stocks, 5-min updates:
- Use NSE API for live prices (most reliable)
- Cache yfinance data (PE, dividend, 52-week) every 1 hour
- Update historical metrics daily

---

## 🔧 Customization

### Change Update Frequency
In Code.gs, modify trigger:
- Every 5 minutes (recommended for live prices)
- Every 30 minutes (if using slower APIs)
- Every hour (for daily snapshots)

### Add More Stocks
In `fetchNSEData()` function, add symbols:
```javascript
const stocks = [
  'RELIANCE', 'TCS', 'HDFCBANK', 'INFY', 'BAJAJFINSV', 
  'SBIN', 'AXIS', 'ITC', 'KOTAKBANK', 'NESTLEIND',
  'WIPRO', 'SUNPHARMA', 'DRREDDY', 'MARUTI'  // Add more here
];
```

### Customize Admin Dashboard
Edit the HTML → Search for `dashboardSettings` in the logic class:
```javascript
dashboardSettings: {
  showProfit1d: true,      // Toggle 1-day returns
  showProfit7d: true,      // Toggle 7-day returns
  showProfit3y: false,     // Toggle 3-year returns
  showManagement: true,    // Toggle management info
  showGrowth: true,        // Toggle growth metrics
  showFivePoints: true     // Toggle 10 growth drivers
}
```

---

## 🎯 Making it 10/10 Rating

### UI/UX Enhancements
✅ Gradient headers & hero cards  
✅ Responsive grid layouts  
✅ Color-coded performance metrics  
✅ Smooth tab transitions  
✅ Mobile-friendly design  

### Data Accuracy
✅ Real-time NSE pricing  
✅ Auto-updated every 5 mins  
✅ Historical profit metrics  
✅ Management team details  
✅ 10 growth drivers per stock  

### Features
✅ Admin dashboard settings  
✅ Stock details view  
✅ Search & sort capabilities  
✅ Profit metrics (1d–inception)  
✅ LocalStorage for preferences  

### Performance
✅ No external bundles  
✅ Pure HTML/CSS/JS  
✅ Instant load time  
✅ GitHub Pages CDN  

---

## 🐛 Troubleshooting

### Data not updating?
- Check Google Apps Script → Executions tab for errors
- Verify GitHub token is valid
- Check repo name matches Code.gs

### Website not loading?
- Wait 5 mins after first deploy
- Clear browser cache (Ctrl+Shift+Del)
- Check repo is public
- Verify index.html in root folder

### NSE API not working?
- API is sometimes rate-limited
- Fall back to static data in Code.gs
- Use yfinance as secondary source
- Contact NSE for higher limits

### GitHub token expired?
- Generate new token in GitHub settings
- Update Code.gs with new token
- Re-deploy Google Apps Script

---

## 📱 Deployment Checklist

- [ ] GitHub repo created
- [ ] Code.gs configured with token
- [ ] Google Apps Script deployed
- [ ] Folder structure (data/, etc.) created
- [ ] index.html uploaded
- [ ] GitHub Pages enabled
- [ ] Trigger scheduled (5 mins)
- [ ] First manual run successful
- [ ] Website live & working
- [ ] Admin settings tested

---

## 🎓 Next Steps

1. **Add more stocks** – Include entire Nifty 50
2. **Implement alerts** – Email for stock crossing targets
3. **Add portfolio tracker** – Users can create watchlists
4. **Export to CSV** – Download analysis & bookmarks
5. **Dark mode** – Toggle in admin settings
6. **Multi-language** – Hindi/Regional language support
7. **Mobile app** – React Native version
8. **Social sharing** – Share analysis on Twitter/LinkedIn

---

**Your 10/10 Indian Stock Analysis website is live! 🚀**
