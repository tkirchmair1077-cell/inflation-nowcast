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

- `schema_version` (currently `"1.1"` for `circular_financing`, `"1.0"` for `token_demand`)
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

- `status`: `current_user_alert`, `summary` (short pulse string), `last_scan`, `last_independent_check`, `outstanding_watches[]`
- `summary`: object written by the AI Circular Financing Alert Bot for the overview box **AI Circular Financing – current state**. Shape: `{ "text", "as_of", "source" }`. `text` is a 4–6 sentence current-state summary from the latest scan and independent check, with V / U / (d) labels on figures and no invented facts. `as_of` is ISO 8601 with a Europe/Zurich offset. `source` names the scan or check used. The page renders this object from the JSON; the bot overwrites it on later scans.

Required date order: circular-financing alerts must **always** be listed newest first.

- Prefer `event_time` when present, otherwise `as_of` (or `date` on outstanding watches). Date-only values (`YYYY-MM-DD`) sort as the start of that calendar day in Europe/Zurich, so a same-day item that carries a time appears first.
- Items with no date go last and must be flagged (`No date`).
- The page sorts at **render time** in `index.html`. Do not rely on JSON array order.
- Still write `items[]` (and `outstanding_watches[]`) newest-first in this feed so other readers of the file follow the same rule. Date is the first column on the deals table.

- `items[]`: deals and relationships. Each item has `id`, `node`, `type`, `title`, `as_of`, `tier_relevance`, `tone`, `tone_source`, `relationship`, `counterparties[]`, `figures[]` (`label`, `value`, `unit`, `quality`, optional `note`), `sources[]` (`title`, `url`, `kind` = `primary` | `secondary`), `notes`
  - `tone`: `positive` | `neutral` | `negative`, from the perspective of AI circular-financing risk. **Positive** (green) = de-risking or healthy financing news. **Negative** (red) = rising circularity, stress or credit risk. **Neutral** (yellow) = mixed or informational. The page shows a badge and a left border, plus a legend in section 2. Outstanding watches may carry the same fields.
  - `tone_source`: `bot` if the AI Alert bot supplied the tone in its saved output; `derived` if it was classified from the item text and the latest scan notes (the bot has no per-item tone field in the 11 Nov 2026 files). Prefer the bot's own tone when it exists.
- `combined_links[]`: short connections to the token-demand feed (`id`, `title`, `text`)
- `source_files[]` (optional, box paths; not shown on the page)

### `data/token_demand.json`

Recommended top-level keys:

- `edition`, `title`, `bottom_line`, `sources_retrieved`
- `readings[]`: headline numbers (`id`, `label`, `value`, `unit`, `quality`, optional `wow_pct`, `note`, `source_url`, `as_of`)
- `crack_watch[]`: `{ id, title, status, text }`
- `series`: named objects, each with `id`, `title`, `unit`, `quality`, `source_url`, `retrieved`, `notes`, `points[]`
  - `openrouter_weekly.points[]`: `week_start`, `total_tn`, `free_tn`, `paid_tn`, `wow_pct`, `g4_pct`, `paid_wow_pct`, `complete`
  - `openrouter_weekly.partial_week`: same shape, `complete: false`
  - `openrouter_trailing7d_paid_free.points[]`: `window_end`, `paid_tn`, `free_tn`, `total_tn`
  - `openrouter_author_share_7d.points[]`: `author`, `tokens`, `token_share_pct`, `spend_share_pct`
  - `openrouter_weekly_author_share.points[]`: `week_start`, `complete`, `shares_pct` (by author); `authors[]` gives stack order
  - `openrouter_token_vs_spend_share.points[]`: `author`, `token_share_pct`, `prior_token_share_pct`, `last_spend_share_pct`
  - `portkey_weekly.points[]`: `week_start`, `tokens_tn`, `cost_usd`, `usd_per_mtok`
  - `ramp_tsm_weekly.points[]`: `week_start`, `token_volume`, `token_spend_usd`, `usd_per_mtok`
  - `ramp_tsm_daily_7d.points[]`: `date`, `tokens_tn`, `spend_usd`
  - `ramp_tsm_ppm_daily.points[]`: `date`, `usd_per_mtok`
  - `ramp_pepm_monthly.points[]`: `month`, `top_1_percent_median`, `top_10_percent_median`, `p90`, `median`
  - `ramp_adoption_monthly.points[]`: `month`, `total_pct`, `mom_change_pp`, `openai_pct`, `anthropic_pct`
  - `vercel_open_weight_traffic.points[]`: `date`, `tokens_daily`, `cost_daily`, `requests_daily`, `tokens_7d`, `cost_7d`, `requests_7d`
  - `vercel_open_weight_preference.points[]`: `date`, `share_pct`, `share_7d`
  - `ramp_tokenomics_table.points[]`: `metric`, `week_ending_latest`, `week_ending_compare`, `value_latest`, `change`, `retrieved`
  - `npm_coding_agent_windows.points[]`: `package`, `window`, `downloads`, `compare_window`, `change_pct`

- `hyperliquid`: live HIP-3 perpetual quotes for Anthropic and OpenAI confirmed from the public Hyperliquid info API (`as_of`, `markets[]`, `series`, `notes`, `source`). Do not invent tickers. Implied fully diluted valuation is derived only for Entropy `io:` markets, where official docs define $1 as $1 billion of FD valuation. Per-share contracts (`xyz:ANT`, `para:ANTH`) are stored as USD marks only. Flag thin markets. Delisted and unrelated spot tokens are not live issuer quotes.
- `prediction_markets`: curated public Polymarket and Kalshi contracts on OpenAI and Anthropic (`as_of`, `markets[]` with yes-probability, volume, resolution date, link, thin flag; `series` for chart history). Confirm titles and tickers from the APIs. Yes-probabilities are API-read contract prices, not forecasts. Do not include contracts whose titles name underwriting banks.

- `bot_charts`: catalog of the 8 Nov 2026 pack charts redrawn on the page (`intro`, `items[]` with `id`, `pack_file`, `title`, `caption`, `source`, `quality`, `derived`, `as_of`)

The page charts whatever series are present and leaves a “no data” notice if a series is missing. It does not invent points. Public-safe Token Demand pack charts are redrawn in Chart.js from these series; screenshots of third-party documents or sites and charts built on credit-terminal or licensed prints are not included.

The overview (section 1) also shows the Hyperliquid implied-valuation and per-share charts, plus pack charts 01 and 04, on separate canvas IDs. Pack chart 01 is OpenRouter weekly token volume and growth. Pack chart 04 is Ramp price per million tokens and heavy-user PEPM. The same charts remain in section 3.

## Public-page leak check

Before publishing, grep the four publish files (`index.html`, `README.md`, `data/circular_financing.json`, `data/token_demand.json`) so they do not contain licensed or internal-only material. Do not publish `_build/excluded_internal.json`. From this folder:

```
rg -n -i -f _build/leak_patterns.txt index.html README.md data/circular_financing.json data/token_demand.json
```

`_build/leak_patterns.txt` (not published) lists standing-rule source names and distinctive excluded figures from `_build/excluded_internal.json`. Hits must be resolved or justified (for example a generic “excluded” category with no figure).

## This edition (built 11 Nov 2026)

- Circular financing: last scan 11 Nov 2026 ~07:45 Europe/Zurich; independent check ~07:50–08:00. No new Watch-or-higher user alert that morning. Outstanding Watch: Anthropic supplier placement (10 Nov, V). Bank-reluctance item (9 Nov) remains U.
- Token demand: weekly pack dated Sun 8 Nov 2026, 18:32 Europe/Zurich (OpenRouter snapshot 17:42). No later saved pack was found on the box. Section 3 redraws the seven pack charts in Chart.js from the public series. The same section also shows Hyperliquid HIP-3 quotes and curated Polymarket/Kalshi markets for Anthropic and OpenAI, fetched 11 Nov 2026 (Europe/Zurich) from the public APIs; those blocks have their own `as_of` and do not refresh the 8 Nov pack. Section 1 repeats the Hyperliquid charts and pack charts 01 and 04.
- Circular-financing tones on the 11 Nov 2026 items are `tone_source: derived` (the bot files had no per-item tone field). The overview current-state box is the top-level `summary` object, as of the 11 Nov independent check (~08:00 Europe/Zurich).

Internal and licensed material was left out of both JSON files. Public `excluded` entries are generic categories only; the detailed list is not published.
