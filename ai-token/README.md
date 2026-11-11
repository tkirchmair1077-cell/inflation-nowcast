# AI Circular Financing & Token Demand dashboard

Public research page that combines two existing bot feeds in one single-file HTML dashboard, intended for GitHub Pages.

This folder is the publish set. Do **not** invent or refresh figures here: each bot updates only its own JSON file from data it has already saved.

## Files to publish (repo root)

| Path | Role |
|------|------|
| `index.html` | The page (HTML + CSS + vanilla JS, Chart.js 4.4.1 via CDN). Embeds a fallback copy of both feeds and, when served over HTTP, tries to fetch the JSON files. |
| `data/circular_financing.json` | Feed owned by the AI Circular Financing Alert Bot (`eb77e684-7673-4ac6-b399-3377e0af4258`). |
| `data/token_demand.json` | Feed owned by the Token Demand Bot (`1ff4ca99-21f4-48d1-a702-c2ad3bc5fe5d`). |
| `README.md` | This file (schema and update rules). |

Screenshots in `screens/` and the generator in `_build/` are working files, not required on GitHub Pages.

There is no refresh button. Nothing on the page randomises numbers. If a browser shows a stale GitHub Pages copy (cache-control max-age=600), a hard reload or `?v=N` on the URL forces a fresh load.

## Who may write what

- The circular-financing bot may overwrite **only** `data/circular_financing.json`.
- The token-demand bot may overwrite **only** `data/token_demand.json`.
- Neither bot should edit the other file, `index.html`, or this README except to follow a schema change agreed in advance.
- After a JSON update, bump the corresponding `as_of` timestamp (ISO 8601 with explicit offset, Europe/Zurich) and keep `schema_version` current. Rebuild the embedded fallback in `index.html` with `_build/embed_data.py` so file:// and first paint stay in sync, then republish both the JSON and `index.html`.

## Shared conventions

Every feed must include:

- `schema_version` (currently `"1.0"`)
- `feed`: `"circular_financing"` or `"token_demand"`
- `bot.name`, `bot.id`
- `as_of`: ISO 8601 with offset, e.g. `"2026-11-11T07:50:00+01:00"`
- `timezone`: `"Europe/Zurich"`
- `caveats`: array of strings (these are merged into the page’s highlighted «Datenlage und Quellen – Vorbehalte» block)
- `excluded`: array of `{ "item", "reason" }` for anything left off the public page

Quality labels, used on every figure:

- **V** — verified from a primary document that was opened
- **U** — unverified (secondary, anonymous, undated, or not independently confirmed)
- **(d)** — derived / own arithmetic from stated figures

Do not put licensed bank or broker research, paid or licensed datasets, or other internal-only material into these public JSON files. The `excluded` array must use generic categories only: no figures, no broker or bank names tied to figures, and no internal file names. The detailed exclusion list lives only in `_build/excluded_internal.json`, which is not published.

### `data/circular_financing.json`

Recommended top-level keys:

- `status`: `current_user_alert`, `summary`, `last_scan`, `last_independent_check`, `outstanding_watches[]`
- `items[]`: deals and relationships. Each item has `id`, `node`, `type`, `title`, `as_of`, `tier_relevance`, `relationship`, `counterparties[]`, `figures[]` (`label`, `value`, `unit`, `quality`, optional `note`), `sources[]` (`title`, `url`, `kind` = `primary` | `secondary`), `notes`
- `combined_links[]`: short connections to the token-demand feed (`id`, `title`, `text`)
- `source_files[]` (optional, box paths; not shown on the page)

### `data/token_demand.json`

Recommended top-level keys:

- `edition`, `title`, `bottom_line`, `sources_retrieved`
- `readings[]`: headline numbers (`id`, `label`, `value`, `unit`, `quality`, optional `wow_pct`, `note`, `source_url`, `as_of`)
- `crack_watch[]`: `{ id, title, status, text }`
- `series`: named objects, each with `id`, `title`, `unit`, `quality`, `source_url`, `retrieved`, `notes`, `points[]`
  - `openrouter_weekly.points[]`: `week_start`, `total_tn`, `free_tn`, `paid_tn`, `wow_pct`, `complete`
  - `openrouter_weekly.partial_week`: same shape, `complete: false`
  - `openrouter_trailing7d_paid_free.points[]`: `window_end`, `paid_tn`, `free_tn`, `total_tn`
  - `openrouter_author_share_7d.points[]`: `author`, `tokens`, `token_share_pct`, `spend_share_pct`
  - `portkey_weekly.points[]`: `week_start`, `tokens_tn`, `cost_usd`, `usd_per_mtok`
  - `ramp_tsm_weekly.points[]`: `week_start`, `token_volume`, `token_spend_usd`, `usd_per_mtok`
  - `ramp_tokenomics_table.points[]`: `metric`, `week_ending_latest`, `week_ending_compare`, `value_latest`, `change`, `retrieved`
  - `npm_coding_agent_windows.points[]`: `package`, `window`, `downloads`, `compare_window`, `change_pct`

The page charts whatever series are present and leaves a “no data” notice if a series is missing. It does not invent points.

## This edition (built 11 Nov 2026)

- Circular financing: last scan 11 Nov 2026 ~07:45 Europe/Zurich; independent check ~07:50–08:00. No new Watch-or-higher user alert that morning. Outstanding Watch: Anthropic supplier placement (10 Nov, V). Bank-reluctance item (9 Nov) remains U.
- Token demand: weekly pack dated Sun 8 Nov 2026, 18:32 Europe/Zurich (OpenRouter snapshot 17:42). No later saved pack was found on the box.

Internal and licensed material was left out of both JSON files. Public `excluded` entries are generic categories only; the detailed list is not published.
