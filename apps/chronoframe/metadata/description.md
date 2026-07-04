# ChronoFrame

Self-hosted **personal photo gallery** (Nuxt) — smooth display + management of large images,
EXIF parsing, geolocation recognition, and map exploration.

## This deployment (Aethryl custom store)

- **Storage:** `local` provider (upstream default is `s3` — overridden). Photos + DB live under
  the app-data volume `${APP_DATA_DIR}/data` → `/app/data` (local for now, not on the NFS vault).
- **Secret:** `NUXT_SESSION_PASSWORD` (32-char) injected via host
  `user-config/addons/chronoframe/app.env` as `CHRONOFRAME_SESSION_PASSWORD` — never committed.
- **Admin:** auto-created on first boot as `fabianrutten@gmail.com`, default password `CF1234@!` —
  **change on first login** (no self-serve wizard).
- **Reach:** `http://192.168.178.138:8500` on the LAN (main container internal :3000).

Upstream: <https://github.com/HoshinoSuzumi/chronoframe>
