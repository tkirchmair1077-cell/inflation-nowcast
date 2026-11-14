# Inflation breadth — US (v1, public package)

- **Data date:** 2026-09 (monthly)
- **Share above threshold:** 62.2% (d, unrounded 62.151267)
- **Share below threshold:** 21.4% (d, unrounded 21.405448)
- **Diffusion (above − below):** +40.7 pp (d)
- **Z-score of diffusion vs 2011–2019:** +2.47 (d)
- **Thresholds:** strict > 3% / < 1%
- **Component count (n used / n target):** 178 / 182
- **Breaks / sample notes:** Official gaps in the NSA 12-month rate for October 2025 and October 2026 (n/a, BLS shutdown / not yet published at component level). The series used here starts in January 2011; earlier official relative-importance vintages are n/a in the snapshots used.

**Method (d):** Weighted share of official CPI-U leaves, using official linked NSA 12-month rates and December prior-year relative-importance weights on the official leaf cut, renormalised each month.

Shares, diffusion and the z-score are authors' calculations (d) from official linked NSA indexes and official basket weights (V), renormalised each period over items with a published rate and a strictly positive weight. Thresholds are strict (`>` / `<`). This is a research prototype, not a sealed nowcast and not a trade input.
A separate comparison panel of Australia, New Zealand and Canada is in `comparison_au_nz_ca_inflation_breadth.png`, with latest values in `comparison_latest.csv` / `comparison_latest.json`. See `comparison_caption.md` for those thresholds, component counts, data dates and caveats.

Credit and licence: see `credit.md`.

«Datenlage und Quellen – Vorbehalte»: see `vorbehalte.md`.
