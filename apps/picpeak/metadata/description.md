# PicPeak

Self-hosted **client photo delivery / proofing** galleries — an open-source alternative to
Pixieset / PicDrop for professional photographers.

- Optional per-gallery password (auth is opt-in, not mandatory)
- Time-limited galleries (expiry)
- Client favorites / proofing / selection
- Full-resolution + bulk ZIP downloads
- Watermarking, white-label branding, custom domain
- View/download analytics

## This deployment (Aethryl custom store)

- **Storage:** bulk photos live on the redundant **vault RAID** share, bound into LXC 104 as
  `/galleries` (host `/mnt/pve/files/client-galleries`). PicPeak writes `events/<gallery>/` there.
- **Secrets:** `PICPEAK_JWT_SECRET`, `PICPEAK_DB_PASSWORD`, `PICPEAK_REDIS_PASSWORD` are injected
  via the host `user-config/addons/picpeak/app.env` (never committed).
- **Services:** `frontend` (main, :80) → proxies `/api` + `/uploads` to `backend` (:3000);
  `postgres:15`, `redis:7` for state.
- **Exposure:** public at `galleries.spaceserver.stream` via Nginx Proxy Manager.

Upstream: <https://github.com/the-luap/picpeak> · <https://picpeak.app>
