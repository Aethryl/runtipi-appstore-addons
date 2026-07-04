# Photoview

Self-hosted **personal photo library** — scans a read-only media folder into a timeline and
albums, with EXIF, an optional Mapbox map, face recognition, and RAW + video support.

- Timeline + album browsing of your own collection
- EXIF metadata, map/Places (needs a free `MAPBOX_TOKEN`)
- Face recognition, RAW processing, video encoding
- Media folder is mounted **read-only** — Photoview never writes to your originals

## This deployment (Aethryl custom store)

- **Backend:** SQLite (single container) — DB at `${APP_DATA_DIR}/database`, thumbnail/video cache
  at `${APP_DATA_DIR}/media-cache`. Both are LXC-local (add to backups), pre-chowned to uid `999`.
- **Library:** the personal **`Fotos`** tree on the redundant **vault** pool
  (`/mnt/pve/files/stack_storage/Fotos`), bind-mounted into LXC 104 as `/photos` and into the
  container `/photos:ro`. Scoped to `Fotos` only — the `stack_storage` root also holds private
  backups/secrets that must NOT be exposed.
- **First run:** create the admin user in the browser, then set the scan path to `/photos` on the
  init page. No headless admin (Photoview has no env-admin bypass).
- **Secrets:** optional `PHOTOVIEW_MAPBOX_TOKEN` via host `user-config/addons/photoview/app.env`
  (never committed).
