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

Checking what is actually live, concretely for this site:

```bash
curl -s -o /dev/null -w 'HTTP %{http_code}\n' https://vinaigresque.com/
```

That is all the page will tell you from outside. **The page carries no build
stamp on purpose**, so a 200 proves the endpoint answered and nothing more —
which commit is serving can only be read on the droplet:

```bash
vinaigresque status     # checkout SHA, live probe, cert days
```

The platform conventions say to ask for the deployed commit rather than just
the status code. On this site that ask has to happen on the box; there is no
remote answer, because a remotely readable stamp is a publicly readable one
and this site would rather not publish it.

## Things worth knowing

- The droplet checkout is the web root, so anything committed here is public
  except dotfiles and `*.md` (the vhost denies both). Don't commit secrets;
  there is no `.env` on a static site.
- There is no `.env` here and nothing to keep out of git beyond that — a
  static site has no secrets to hold.
