# Fed Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved note. Do not invent numbers.
- `charts/` — US CPI nowcast-versus-actual backtest chart, drawn from the already-produced 6 Nov 2026 inflation-nowcast model backtest. No new model is estimated.
- `README.md` — this file.

**As of:** 12 Nov 2026, 07:40 Europe/Zurich
**Source:** IPDeck_US_nowcast_note_2026-11-12.md

Omitted from this public page: third-party inflation-nowcast model readings; survey-consensus figures and surprises; secondary unofficial PCE estimates; licensed bank, broker and private-survey datasets. Claims for the week ended 7 Nov were still missing at the cutoff. The core PCE baseline awaits PPI on 13 Nov before any reset.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment.

This page is a staff-style research compilation, not official central-bank staff work. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.
