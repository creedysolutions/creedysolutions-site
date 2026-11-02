# STOP: do not deploy this folder directly

creedysolutions.com runs the **redesign**. This folder is still where the content lives (pages, guides, images,
`/media`, feeds), so keep editing here as usual, but it is **not** what gets deployed anymore.

Running `wrangler pages deploy` from here (or uploading this folder to the `creedysolutions` Pages project any
other way) puts the OLD design back on the live site. That happened once already (2026-11-01).

## How to publish a change

1. Make the change here (edit a page, add a guide, drop files into `media/` or `assets/`).
2. From `~/Documents/CreedySolutions/sites/creedysolutions-redesign`:

   ```bash
   node remake/rebrand/products.mjs && python3 remake/rebrand/release.py
   cd dist/creedysolutions && npx wrangler@4 pages deploy . --project-name creedysolutions --branch main --commit-dirty=true
   ```

   The build restyles the pages, merges in every other file from this folder unchanged, and checks the
   result before anything ships.

Details, rollback and the full rules: `creedysolutions-redesign/KEEP.md`, section 0.
Not covered here: fawnhaven.creedysolutions.com is a separate project and stays exactly as it is.

Deploy from INSIDE `dist/<site>` as shown: wrangler reads `./functions/` from the current directory, and the
redesign repo root has the preview passcode gate there, which must never reach production.
