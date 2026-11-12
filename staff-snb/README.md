# SNB Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved baseline note. Do not invent numbers.
- `charts/` — official BFS CPI (headline, core 1, domestic, imported y/y); the SNB September 2026 conditional inflation forecast versus actual CPI; official weekly sight deposits; official monthly EUR/CHF and USD/CHF (SNB cube devkum); and a LIK month-on-month benchmark backtest (benchmarks only; the component model is pending). Charts are drawn from already-produced official series and the already-produced 12 November 2026 benchmark backtest. No new model is estimated.
- `README.md` — this file.

**As of:** 12 Nov 2026 (no time of day was recorded on the note)
**Source:** SNB baseline note, 12 November 2026

Omitted from this public page: SNB daily exchange rates computed from Bloomberg BFIX (licensed origin; official monthly FX is shown instead); market-implied SNB pricing (not obtained; not estimated); an unsealed LIK component-nowcast prototype; third-party FX-intervention reports; SIX official six-decimal SARON (not fetched); licensed bank, broker and private-survey datasets; survey-consensus figures. The staff baseline for 10 December is a hold at 0%. A staff LIK nowcast point is not published.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment (the hawk/dove score is an Einschätzung, keine Formel).

This page is a staff-style research compilation, not official Swiss National Bank staff work and not a Governing Board projection. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.
