# Fed Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved notes. Do not invent numbers.
- `charts/` — US CPI nowcast-versus-actual backtest, drawn from the already-produced 6 Nov 2026 inflation-nowcast model backtest (no new model is estimated); 15 leading-indicator charts (inflation, labour, growth) from the Fed Staff Desk note of 12 Nov 2026, 17:24 Europe/Zurich; and seven 10-year Treasury composition charts refreshed 13 Nov 2026, 06:47 Europe/Zurich (H.15 and ACM through 10 Nov; Kim-Wright through 6 Nov). The publish set does not include any file with INTERNAL in its name.
- `README.md` — this file.

**As of:** 12 Nov 2026, 07:40 Europe/Zurich (nowcast note). Leading-indicator section: 12 Nov 2026, 17:24 Europe/Zurich. 10-year Treasury composition: H.15 and ACM 10 Nov 2026; Kim-Wright 6 Nov 2026 (fetched 13 Nov 2026, 06:47 Europe/Zurich, after the 12 November 22:15 H.15 slot).
**Source:** IPDeck_US_nowcast_note_2026-11-12.md; leading_indicators_2026-11-12.md (leading-indicator charts and staff reads); ust10y_decomposition_charts_2026-11-12.md (10-year composition charts and staff read).

Page section order: 1 Current state; 2 Staff view; 3 Leading indicators (three blocks: Inflation, Labour, Growth, each with a staff read versus the 6 Nov baseline); 4 10Y Treasury: where the move comes from (Split A market, Split B ACM and Kim-Wright); 5 Nowcasts; 6 Baseline; 7 Key data since last update; 8 Upcoming calendar; 9 Charts (CPI backtest).

Atlanta Fed BIE, the Richmond Fed survey price series (as a staff chart, including an equal-weight staff construction (d) of prices received, not an official index) and the Federal Reserve Bank of Cleveland 1-year expected inflation series (noncommercial, DOI https://doi.org/10.26509/frbc-infexp) are on this public page with credit lines, following Thomas’s 12 Nov 13:52 decision. Every leading-indicator chart carries a source credit and a “Shown without endorsement by …” line.

The 10-year composition uses a staff breakeven (d) equal to DGS10 minus DFII10 on the same H.15 vintage (FRED T10YIE is not used), NY Fed ACM with the product URL and official-estimates disclaimer, and Board Kim-Wright (feds200533) with the staff-product notice. The 1-day Kim-Wright waterfall panel is flagged STALE. A model-based 10-year expected-inflation companion is held off this public page under the house rule and is not in this publish set.

Omitted from this public page: third-party inflation-nowcast model readings; survey-consensus figures and surprises; secondary unofficial PCE estimates; licensed bank, broker and private-survey datasets. The leading-indicator labour charts include the advance initial claims for the week ended 7 Nov (revises 19 Nov). The core PCE baseline awaits PPI on 13 Nov before any reset.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment.

This page is a staff-style research compilation, not official central-bank staff work. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.
