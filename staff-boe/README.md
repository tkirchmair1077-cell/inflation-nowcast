# BoE Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved note. Do not invent numbers.
- `README.md` — this file.

**As of:** 8 Nov 2026, 09:00 Europe/Zurich — several days old
**Source:** BoE Staff Desk report, 8 Nov 2026; charts generated the same day from ONS and Bank of England Decision Maker Panel data

Also publish `charts/uk_leading_indicators_2026-11-08.png` and `charts/uk_nowcast_vs_mpr_2026-11-08.png`.

Omitted: private business-survey (PMI) figures; survey-consensus figures; licensed datasets. There is no approved desk baseline. Q3 and September GDP were due 12 Nov and are not incorporated on this page. October CPI is due 18 Nov and labour-market data 17 Nov.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment.

This page is a staff-style research compilation, not official central-bank staff work. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.

No inflation nowcast-versus-actual backtest has been produced by the BoE Staff Desk; the page states this visibly. The existing charts compare a current nowcast with official Bank of England projections, which is not a backtest.
