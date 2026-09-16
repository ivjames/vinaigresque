# Vinaigresque

A mustard-free vinaigrette mix. This repo is the site at
**https://vinaigresque.com** — a single static landing page, light mode only.

- **Shape:** fully static. One `index.html`, no build step, no app process, no
  port, no pm2, no database. nginx on the lab980 droplet serves this checkout
  directly.
- **Working agreement:** `CLAUDE.md` (and `.claude/rules/lab980-conventions.md`
  for the platform-wide conventions). Changes land through a pull request.
- **Deploying:** `DEPLOY.md`. Merging does **not** deploy — `vinaigresque deploy`
  on the droplet does.
