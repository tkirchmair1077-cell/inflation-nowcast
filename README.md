# Inflation Nowcasts dashboard (REAL DATA, 11 Nov 2026)

Single file: `index.html` (HTML + CSS + vanilla JS, Chart.js 4.4.1 via CDN). All numbers come from `const NOWCAST_DATA` at the top of the script (a copy is in `../_build/nowcast_data_real.json`; generator `../_build/make_real.py`).

* US CPI (Oct 2026): sealed freeze of 10 Nov 2026 vs BLS first release; status YELLOW. PPI (Oct 2026): unsealed stage-B1 run of 11 Nov 2026, status not audited. PCE: no nowcast available (shown as "no data").
* Sections without real data say "no data" (evolution, y/y, consensus history, PCE).
* The simulated "Refresh" button was removed (hidden) because it perturbed numbers randomly.
* Old example version: `_backup/index_example.html` (example data, with screenshots in `_backup/screens_example/`).
* Screenshots of the real version: `screens/real-*.png`.
* Internal-only content is NOT on the page.

https://tkirchmair1077-cell.github.io/inflation-nowcast/
