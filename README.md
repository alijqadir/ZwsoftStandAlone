# ZWSOFT standalone (Hugo)

This is a single-page Hugo site for the ZWSOFT landing page. The entire page lives in `static/index.html` with its supporting assets in `static/css`, `static/js`, and `static/images`.

## Run locally
1. Install Hugo (extended) if you don't have it.
2. From this folder, run:
   ```bash
   hugo serve --disableFastRender
   ```
3. Open the served URL (usually http://localhost:1313). The page is fully static; Hugo just hosts it.

## Deploy
- Host the `public/` output after running `hugo` or simply upload the `static/` contents to any static host (it is already a complete site).
- Update `hugo.toml` `baseURL` with your target domain/subdomain if you plan to run `hugo` builds.

## SEO + analytics
- `static/robots.txt` and `static/sitemap.xml` are included; update `hugo.toml` `baseURL` (and the URLs inside those files) to your production domain before building so search engines see the right links.
- Set `params.tracking.gaId` to your GA4 measurement ID and adjust `adsId`/`adsLabel` as needed. You can also override these at build time with env vars (`HUGO_PARAMS_TRACKING_GAID`, `HUGO_PARAMS_TRACKING_ADSID`, `HUGO_PARAMS_TRACKING_ADSLABEL`).
- After changing config, run `hugo` to refresh `public/`, then commit and push.

## GitHub Pages auto-deploy
- A workflow at `.github/workflows/deploy.yml` builds the site with Hugo and deploys to GitHub Pages on every push to `main`.
- In repo Settings → Pages, set Source to GitHub Actions.
- Add repository variables for `SITE_BASEURL` (your live URL with trailing slash) plus optional `GA_ID`, `ADS_ID`, and `ADS_LABEL` so the workflow can stamp the correct base URL and analytics IDs at build time.
- Push to `main` (or run the workflow manually) to publish the updated site.

### Optional: deploy to your own server
- For FTP/FTPS deploys, add secrets in Settings → Secrets → Actions: `FTP_HOST`, `FTP_USERNAME`, `FTP_PASSWORD`, `FTP_PATH` (destination directory), and optionally `FTP_PORT` (default 21). The workflow uses FTPS by default.
- On each push to `main`, the workflow will upload the built `public/` folder to `FTP_PATH` when the FTP secrets are set.

## Notes
- Forms post to the same Google Apps Script endpoint used in the original site. If you change the destination, edit `static/js/form-to-sheets.js` and the inline form handler inside `static/index.html`.
- Assets are all relative (no leading slashes), so the site works from any domain or subpath.
