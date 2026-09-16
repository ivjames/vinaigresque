# Deploying Vinaigresque

Target: **https://vinaigresque.com** — served from the lab980 droplet (conventions in
the `ivjames/lab980.com` repo's `CLAUDE.md`).

The site is static files with no dependencies: no build step, no app process,
no port, no pm2, no database. nginx serving the git checkout *is* the
deployment. Everything is driven by the operate CLI at `bin/vinaigresque`.

> Why not `provision-site`? That script scaffolds proxy-shaped sites (an app on
> a local port). This site has no app, so `vinaigresque setup` writes its own
> static vhost instead — same DNS/doctl, security-headers and certbot shape.

## One-time bring-up (on the droplet, as root)

```bash
git clone https://github.com/ivjames/vinaigresque /var/www/vinaigresque
ln -sf /var/www/vinaigresque/bin/vinaigresque /usr/local/bin/vinaigresque
vinaigresque setup
```

`vinaigresque setup` is idempotent and does, in order:

1. **DNS** — `doctl` A records for `vinaigresque.com` (record `@`) **and**
   `www.vinaigresque.com`, both pointing at the droplet IP. Each is skipped if
   it already exists, so this is safe to run against a zone that is already
   correct; `--no-dns` skips the step entirely, `--no-www` drops the www half,
   `--ip` overrides autodetection.

   **Both records already resolved to 165.22.128.19 on 2026-09-16**, checked
   from outside the droplet. What has *not* been confirmed is that the zone is
   managed in DigitalOcean — if it is hosted at the registrar instead, `doctl`
   will not find it and this step fails. Run `doctl compute domain list | grep
   vinaigresque` first; if it is absent, either
   `doctl compute domain create vinaigresque.com` (and repoint the
   nameservers) or simply run `vinaigresque setup --no-dns`, since the records
   the step would create already exist.
2. **nginx** — static vhost from `deploy/nginx.conf.template` installed as
   `/etc/nginx/sites-available/vinaigresque.com`, symlinked into `sites-enabled/`,
   with `server_name vinaigresque.com www.vinaigresque.com` (the apex shape
   `provision-site @` uses: one vhost naming both, no redirect between them),
   `nginx -t` + reload. Root is the checkout; `index.html` is served
   `Cache-Control: no-cache` so deploys are live on the next visit; dotfiles
   and `*.md` are denied. An existing vhost is left untouched (certbot owns it
   after TLS).
3. **TLS** — waits for DNS to resolve, then
   `certbot --nginx -d vinaigresque.com -d www.vinaigresque.com --redirect -n`,
   one cert covering both names. If DNS is still propagating it prints the
   exact certbot command to re-run.

## Deploying updates

Land changes on `main` (via a PR — see `CLAUDE.md`), then on the droplet:

```bash
vinaigresque deploy
```

That is `git fetch` + `git reset --hard origin/main` of the checkout. No build,
no restart, no reload. The CLI will also stamp the deployed commit into a
`BUILD` constant if the page carries one — this page deliberately does not, so
that step is a no-op here.

## Check it

```bash
vinaigresque status              # HEAD commit, live probe, cert days
health-check --site vinaigresque # the droplet-wide auditor also covers it
```

## Overrides

- `VINAIGRESQUE_FQDN` — serve under a different name (default `vinaigresque.com`)
- `VINAIGRESQUE_BRANCH` — deploy a different branch (default `main`)
- `VINAIGRESQUE_ZONE` / `VINAIGRESQUE_RECORD` — override the DNS split
  (default: zone `vinaigresque.com`, record `@`)
- `VINAIGRESQUE_WWW=0` — leave `www.vinaigresque.com` out of DNS, the vhost
  and the cert (same as `setup --no-www`)

## Notes specific to this site

- **It is an apex domain, not a `*.lab980.com` subdomain.** That only changes
  the DNS split (zone `vinaigresque.com`, record `@`) and the www alias; the
  one-dir-per-site, operate-CLI, shared-security-headers and per-site-certbot
  conventions are unchanged.
- **The dotfile deny in `deploy/nginx.conf.template` uses the lookahead form**
  `location ~ /\.(?!well-known)`, not the bare `location ~ /\.` the lab980
  static template still emits. The bare form also denies
  `/.well-known/acme-challenge/`, which is where certbot serves its HTTP-01
  challenge — it would break the `setup` run's own certbot call and every
  renewal after it. Do not "simplify" it back.
- **The page carries no `BUILD` constant, deliberately.** The deploy stamp is
  optional in the CLI (`deploy` only stamps a page that already has the
  declaration line, and `status` prints `build n/a` without one), and this is
  a product landing page rather than a dashboard — a commit SHA in the footer
  is for us, shown to everyone. The cost is real and worth stating: there is
  no way to tell which commit is live from off the box, because any stamp a
  remote check can read is one every visitor can read. `vinaigresque status`
  on the droplet reports the checkout SHA, and that is now the only answer.
  If you ever want the remote check back, re-add the constant at two-space
  indentation with single quotes — the anchored `sed` in `bin/vinaigresque`
  matches exactly that shape — and put it back in the footer.
