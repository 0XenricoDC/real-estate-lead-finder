# 🏠 Real Estate Lead Finder

> Desktop tool that finds **private sellers** on Italian real-estate portals, filters out agencies, scores every lead 1-100 and exports a prioritized Excel file.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-async-2EAD33?logo=playwright&logoColor=white)
![Tkinter](https://img.shields.io/badge/GUI-Tkinter-FFCC00)
![Excel](https://img.shields.io/badge/export-Excel-217346?logo=microsoftexcel&logoColor=white)

---

## Features

- **Multi-portal search** — Subito.it, Immobiliare.it, Idealista, Casa.it, Bakeca
- **Private-only filter** — agency listings are detected and dropped automatically
- **Lead scoring (1-100)** — price, urgency, margin, listing completeness, listing age and area
- **Official APIs when available** — Idealista and Immobiliare.it clients, scraping as fallback
- **Proxy support & rate limiting** — residential proxies and randomized delays between requests
- **Cross-portal deduplication** — the same property listed on several portals is merged (normalized phone, address, town)
- **Excel export** — leads split by priority, plus a statistics sheet

## Lead scoring

```
SCORE = Price × 0.30 + Urgency × 0.25 + Margin × 0.20
      + Completeness × 0.10 + Listing age × 0.10 + Area × 0.05
```

| Priority | Score |
|---|---|
| 🔴 High | 70 – 100 |
| 🟡 Medium | 40 – 69 |
| ⚪ Low | 1 – 39 |

## Quick start

```bash
pip install -r requirements.txt
playwright install chromium
python main.py            # or double-click avvia.bat on Windows
```

Optional API credentials and proxy settings are read from environment variables / `config.py`:
`IDEALISTA_API_KEY`, `IDEALISTA_API_SECRET`, `IMMOBILIARE_API_KEY`, `PROXY_ENABLED`, `SCORING_WEIGHTS`.

## Project structure

```
main.py            entry point (Tkinter GUI)
config.py          settings, constants, scoring weights
scrapers/          one Playwright scraper per portal (shared async base class)
data_sources/      official API clients (Idealista, Immobiliare.it)
gui/               main window, filters, results table, progress & proxy dialogs
models/            Pydantic models (Lead, SearchFilters)
services/          scoring, cross-portal deduplication, Excel export
```

## Output

An Excel workbook with five sheets: High / Medium / Low priority leads, all leads, and statistics.

## Disclaimer

Respect each portal's terms of service and applicable privacy law (GDPR) when collecting and contacting leads.
