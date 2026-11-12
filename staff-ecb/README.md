# ECB Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved notes. Do not invent numbers.
- `charts/` — ECB wage tracker (ECB Data Portal series, fetched 6 Nov 2026) and euro-area HICP nowcast-versus-actual backtest (already-produced 6 Nov 2026 inflation-nowcast model backtest; no new model is estimated); and 12 leading-indicator charts (inflation, labour, growth) from the ECB Staff Desk public set of 12 Nov 2026, 18:41 Europe/Zurich.
- `README.md` — this file.

**As of:** 12 Nov 2026, 07:50 Europe/Zurich (nowcast note; data cut-off 11 Nov, 17:55 CET). Leading-indicator section: 12 Nov 2026, 18:41 Europe/Zurich.
**Source:** nowcast_ipdeck_2026-11-12.md; leading_indicators_2026-11-12.md (leading-indicator charts and staff reads).

Page section order: 1 Current state; 2 Staff view; 3 Leading indicators (three blocks: Inflation, Labour, Growth); 4 Nowcasts; 5 Baseline; 6 Key data since last update; 7 Upcoming calendar; 8 Charts (wage tracker and HICP backtest).

The leading-indicator charts carry “Staff view, not ECB staff projections.” The AAA 10y–3m spread is labelled a recession-risk indicator, not a growth lead, and the linear-GDP null is stated (staff decision, 12 Nov 2026, 19:31 Europe/Zurich). The wage tracker, ESI and Indeed Hiring Lab posted-wage tracker are labelled coincident/diagnostic. Computed figures are (d) and pseudo-real-time on final vintages. October 2026 HICP is the flash; the final is due on 18 November. A recession probit versus CEPR dates is not yet tested (n/a).

Omitted: a third-party euro-area GDP nowcast tracker marked internal-only; survey-consensus figures; licensed bank, broker and private-survey datasets; EURIBOR (Refinitiv); GSCPI (internal pending clearance). The Q4 HICP own estimate (~3.8–3.9) is pending and has not replaced the ~4.0 baseline. National activity and survey releases from 5–11 Nov are not in the source note.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment.

This page is a staff-style research compilation, not official central-bank staff work. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.
