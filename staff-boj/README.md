# BoJ Staff Desk public page

Publish set for GitHub Pages (`inflation-nowcast/`).

- `index.html` — page (HTML + CSS + vanilla JS). Embeds a fallback copy of `data/desk.json` and, when served over HTTP, tries to fetch the JSON.
- `data/desk.json` — figures and text from the desk’s saved note. Do not invent numbers.
- `README.md` — this file.

**As of:** 1. Nov. 2026 — veraltet
**Source:** Japan-Nowcast im BoJ-Stil, Erstlauf (Page, 1. Nov. 2026) und boj_nowcast_2026-11-01.json

Sprache: Deutsch, wie die Quellenpage.

Ausgelassen: Konsensumfragen, PMI-Flash, OIS-Wahrscheinlichkeiten aus Sekundärquellen, lizenzierte Datensätze. Der Nominallohn-Nowcast für September bezog sich auf die Veröffentlichung am 6.11. und wurde nicht aktualisiert. BIP Q3 ist für den 16.11., der nationale VPI Oktober für den 20.11. vorgesehen. Erstlauf: keine Zerlegung gegenüber einem vorherigen Nowcast.

Quality labels: **V** verified, **U** unverified, **(d)** derived, **own estimate** = staff judgment.

This page is a staff-style research compilation, not official central-bank staff work. Not investment advice. After editing the JSON, run `python3 ../_build/build.py` and `python3 ../_build/leak_check.py`.
