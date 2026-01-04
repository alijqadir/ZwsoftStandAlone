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

## Notes
- Forms post to the same Google Apps Script endpoint used in the original site. If you change the destination, edit `static/js/form-to-sheets.js` and the inline form handler inside `static/index.html`.
- Assets are all relative (no leading slashes), so the site works from any domain or subpath.
