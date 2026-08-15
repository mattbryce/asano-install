# asano-install

Docker Compose files for self-hosting [Asano](https://github.com/mattbryce/Asano)
— the app's own repo is private, so these live here where anyone can `curl`
them without needing access to it.

**`docker-compose.yml`** — the normal starting point. Bundled Postgres, no
`.env` required:

```bash
mkdir asano && cd asano
curl -O https://raw.githubusercontent.com/mattbryce/asano-install/main/docker-compose.yml
docker compose up -d
docker compose logs asano   # read the one-time setup token printed here
```

A bundled Caddy reverse proxy is the public entry point (80/443) — Asano
itself only listens on `localhost`. `http://localhost:3000` works directly
for a local eval; set `SITE_ADDRESS=your-domain.com` in `.env` and restart
for anyone else to reach it, and Caddy gets real, auto-renewing HTTPS with
nothing else to configure. Caddy's own config is inline in the compose file
(a Docker Compose `configs:` entry) rather than a separate file — nothing
else to curl.

**`docker-compose.external-db.yml`** — advanced: point at your own Postgres
from the very first boot, instead of moving to one later via Settings →
Database. See its own header comments for details.

Full install guide (updating, backups, recovering access, environment
variables): open the app and follow the "Installation guide" link on the
setup wizard, or **Help & Feedback → Installation** once signed in — both
render the same guide from the private repo, kept up to date there.

These two files are mirrored here from the main repo whenever they change;
that repo remains the source of truth for editing them.
