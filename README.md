# Fresh-Mill Finder

A static directory and map of small and regional US flour mills and stone-ground flours.

- Data: `mills.csv` (source of truth). Geocode cache: `raw/geocache.json`.
- Build: `python3 site/build.py`, which writes `site/_site/`. Set `BASE_PATH` (default `/freshmillfinder/`) for the 404 page when you host at a different path. All other links are relative.
- Deploy: on each push to `main`, `.github/workflows/pages.yml` builds the site and publishes it to GitHub Pages. In repo Settings → Pages, set Source to "GitHub Actions".
- Map: Leaflet with OpenStreetMap tiles. Map data © OpenStreetMap contributors.
