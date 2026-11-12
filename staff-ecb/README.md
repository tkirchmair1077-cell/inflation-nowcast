# ECB Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved note. Do not invent numbers.
- `charts/` — ECB wage tracker (ECB Data Portal series, fetched 6 Nov 2026) and euro-area HICP nowcast-versus-actual backtest (already-produced 6 Nov 2026 inflation-nowcast model backtest). No new model is estimated.
- `README.md` — this file.

**As of:** 12 Nov 2026, 07:50 Europe/Zurich (data cut-off 11 Nov, 17:55 CET)
**Source:** nowcast_ipdeck_2026-11-12.md

Omitted: a third-party euro-area GDP nowcast tracker marked internal-only; survey-consensus figures; licensed bank, broker and private-survey datasets. The Q4 HICP own estimate (~3.8–3.9) is pending and has not replaced the ~4.0 baseline. National activity and survey releases from 5–11 Nov are not in the source note.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment.

This page is a staff-style research compilation, not official central-bank staff work. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.
