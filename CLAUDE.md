# Vinaigresque — working notes

A mustard-free vinaigrette mix — one static index.html on its own apex domain.

Served at **https://vinaigresque.com** from the lab980 droplet.

How work lands here — branch, PR, and the fact that merging is not deploying —
is in `.claude/rules/lab980-conventions.md`, which Claude Code loads
automatically every session. That file is owned by the lab980 scaffold and is
overwritten by it; **this** file is the site's own, and everything below is
about this site rather than about the platform. For the box itself, read the
`ivjames/lab980.com` repo's `CLAUDE.md`.

## Shape

Fully **static**: the site is files served straight by nginx. No build step,
no app process, no local port, no pm2, no database. nginx serving the git
checkout *is* the deployment, so "what's on `main`" and "what's live" differ
only by a `git reset` on the droplet.

- Repo: `ivjames/vinaigresque` · droplet checkout: `/var/www/vinaigresque` (the web root)
- Operate CLI: `bin/vinaigresque`, symlinked to `/usr/local/bin/vinaigresque`
- vhost: generated from `deploy/nginx.conf.template` by `vinaigresque setup`

## Deploying

On the droplet, as root:

```bash
vinaigresque deploy      # git fetch + reset --hard origin/main (+ build stamp)
vinaigresque status      # HEAD, live probe, cert days remaining
```

Full runbook, including first-time bring-up: `DEPLOY.md`.

Checking what is actually live, concretely for this site — `vinaigresque status`
on the box, or from anywhere:

```bash
curl -s -o /dev/null -w 'HTTP %{http_code}\n' https://vinaigresque.com/
curl -s https://vinaigresque.com/ | grep -o "const BUILD = '[^']*'" | head -1
```

(The second line reports nothing if the page carries no `BUILD` constant — see
the deploy stamp note in `DEPLOY.md`. `head -1` because a page that polls its
own build stamp carries a matching regex literal, which grep otherwise reports
as a phantom second build.)

## Things worth knowing

- The droplet checkout is the web root, so anything committed here is public
  except dotfiles and `*.md` (the vhost denies both). Don't commit secrets;
  there is no `.env` on a static site.
- There is no `.env` here and nothing to keep out of git beyond that — a
  static site has no secrets to hold.
