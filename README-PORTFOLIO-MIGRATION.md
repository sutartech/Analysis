# SutarTech Analysis — SarNi Portfolio Integration (v1.1, TEST RELEASE)

Created using user-uploaded `SarNi-main.zip`, `Analysis-main.zip` and SarNi Google Apps Script backend v3.17.10.

## What changes

- Analysis market research stays in the same `index.html`, with added navigation buttons to Portfolio.
- Four SarNi modules run under `portfolio.html`: **Investment**, **Holdings**, **Transactions**, **SIP Planner**.
- The user keeps the **same SarNi Google Sheet** and the same account/credentials within the separate Portfolio sign-in screen.
- The existing market quote feeder for Analysis remains separate and unchanged.
- The included separate SarNi backend text file bumps v3.17.10 to v3.17.11. It:
  1. Whitelists `https://sutartech.github.io` in addition to `https://saradasutar.github.io` for the faster `postMessage` transport.
  2. Minimises *normal API response data* for the new Analysis Portfolio interface, omitting unrelated household expenses/diary/book contents. This is **not a security boundary**, and legitimate SarNi backend users keep their usual permissions.
  3. Leaves Sheets, schema, authentication and investment calculations unchanged.

## Deployment order (SAFE)

1. Keep a backup of both original frontend ZIPs and the original Apps Script `Code.gs`. Never publish the backend source (including configuration/credentials) to GitHub Pages.
2. Open your *existing SarNi backend Apps Script project*, replace `Code.gs` contents with **SarNi-Backend-v3.17.11-for-Analysis.txt** (downloaded separately). Save.
3. Apps Script: **Deploy → Manage deployments → Edit (pencil) existing web app → Version: New version → Deploy**. Keep **Execute as: Me** and its existing access configuration. Do NOT select New deployment. Record/check the `/exec` URL; if it changes, adjust only the API_URL inside `portfolio.html`.
4. **Do NOT run `setupSystem()` or `resetAdminPassword()`**. No data migration or schema re-initialisation is needed.
5. On GitHub `sutartech/Analysis`, upload the contents of **Analysis-with-SarNi-Portfolio-v1.1-TEST.zip** to the root; replace `index.html`, add `portfolio.html`, `portfolio.js`, `portfolio.css`, `favicon.svg` and the README. Keep original Analysis's existing other files as needed.
6. After GitHub Pages updates, open `https://sutartech.github.io/Analysis/` and click Investment, Holdings, Transactions, SIP Planner.
7. Sign into **Portfolio** with existing **SarNi** credentials (Analysis's existing market app login is separate).
8. Confirm owner names, values, totals, transaction history, SIP plans, filters on mobile and desktop. Test editing with a disposable test record only once read-only checks pass.
9. Verify SarNi is still functioning as before. Remove its old investment navigation only after testing.

## Important differences and caveats

- Portfolio uses the SarNi login; the Analysis market app's existing browser-local login is unrelated. No single-sign-on is provided.
- Analysis market quote feeder (`updateAll`, `setupSheet`) is independent of the **SarNi investment database**, and must not be mixed with SarNi data.
- This frontend reuses much of the original SarNi frontend's UI and JavaScript to preserve investment features. Non-investment menu destinations are disabled or hidden; do not treat this as a hard isolation from SarNi personal data. Version v1.1 also asks the patched backend to omit that personal data from normal Analysis portfolio responses.
- The fast response allowlist recognises the *whole* `sutartech.github.io` origin (browser origins don't include the `/Analysis` path). The original token-based server login is therefore still essential.
- New BE API requests to `clientScope: 'INVESTMENT_ONLY'` depend on the v3.17.11 backend for payload minimisation; on the original v3.17.10 backend the UI should still work via poll fallback but personal data will still be in response payloads.
- The frontend is not confirmed live until it is published, and live write/login tests require the user's active Google Apps Script deployment and account.

## Rollback

- Restore the **original** SarNi `Code.gs` as a new Apps Script deployment version, if necessary.
- Restore the original Analysis `index.html` from `Analysis-main.zip` to hide the new navigation.
- Nothing in this kit deletes or rewrites your existing investment records. Do not remove SarNi modules yet.
