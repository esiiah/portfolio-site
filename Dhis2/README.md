# DHIS2-Style Zambia Malaria Analytics Dashboard (Frontend-Only Demo)

## Description

DHIS2-style dashboard that demonstrates malaria surveillance analytics for Zambia. National indicators are loaded live from the WHO Global Health Observatory (GHO) API. Facility-level views are simulated from a small local JSON file to mimic DHIS2 facility reporting. No backend, no Python — 100% static and designed for portfolio presentation and demonstration of HMIS thinking.

## Why this project?

This project shows how routine health data can become actionable surveillance intelligence: KPIs, maps, facility monitoring, data-quality checks and alerting. It’s built to look and behave like a real DHIS2 analytics workspace so reviewers and hiring committees instantly understand the public-health value.

## Key features

• Live national malaria KPIs from WHO GHO API (Zambia).
• National time-series chart for trend analysis.
• Zambia map context (Leaflet + public GeoJSON).
• Facility Explorer (local synthetic JSON) to show facility-level trends and mini-profiles.
• Simple data-quality module (completeness demo) and one alert rule (mean + 2×SD).
• DHIS2-style windowed UI to mimic a real HMIS analytics workspace.
• Lightweight: HTML, Tailwind CDN, Chart.js, Leaflet.js, vanilla JS.

## Primary data sources

WHO Global Health Observatory (GHO) API — use the MALARIA_COUNTRY resource filtered by SpatialDim = 'ZMB' for Zambia.
Local synthetic file: malaria_facility_demo.json (used to simulate facility-level reporting because WHO does not publish facility data).

## Recommended WHO query

[https://ghoapi.azureedge.net/api/MALARIA_COUNTRY?$filter=SpatialDim](https://ghoapi.azureedge.net/api/MALARIA_COUNTRY?$filter=SpatialDim) eq 'ZMB' and TimeDim eq 2024
Adjust TimeDim to the year you want (2023, 2025, etc.). If MALARIA_COUNTRY is unavailable, use the Indicator endpoint and filter for malaria indicators for Zambia.

## Project structure (exact)

portfolio-site/
Dhis2/
index.html                 # main DHIS2-style dashboard (frontend)
facility.html              # facility profile page
malaria_facility_demo.json # small demo dataset for facility charts
styles.css                 # optional custom CSS tweaks
README.md                  # this file

## How to run locally (fast)

1. Put the Dhis2 folder in your repo or local folder.
2. Run a small static server from inside portfolio-site/Dhis2:
   python -m http.server 8000
3. Open [http://localhost:8000/index.html](http://localhost:8000/index.html) in your browser.
   Note: Browsers may block cross-origin fetches when you open files directly (file://). Running a tiny server avoids that.

## Alerting rule (demo)

The client-side alert uses this rule:
Alert if current positivity >= mean(last 12 months positivity) + 2 × sd(last 12 months positivity).
This is a demonstration of a simple early-warning threshold used in surveillance dashboards.

## Design notes

• The UI mimics DHIS2 with a windowed header, control dots, KPI cards and a central analytics workspace.
• Facility-level data is synthetic: include real facility geometry or district GeoJSON if you have it to improve the map.
• WHO API is the live national source; keep facility JSON local to simulate subnational reporting.

## Limitations

• No official facility-level data is available from WHO; local JSON is a demo only.
• District-level choropleth depends on available district GeoJSON.
• Alerts and calculations are client-side and simplified for demonstration.

## Extending this project

• Replace synthetic facility JSON with a proper DHIS2 export if you have access.
• Add district GeoJSON for a true choropleth.
• Implement server-side indicator aggregation and alerting for production.
• Add CSV export or a lightweight persistence layer if needed.

## Acknowledgements

WHO Global Health Observatory (GHO) for national malaria indicators. Open-source libraries: Chart.js and Leaflet. Design inspired by DHIS2 analytics interface.

## Contact

Esiah Kapinga — esiah_kapinga (portfolio / GitHub / LinkedIn)
If you want a packaged demo (12-month synthetic data added), say “Add demo JSON” and I’ll build it for you.

## License

MIT — feel free to reuse and adapt for portfolio and demo use.
