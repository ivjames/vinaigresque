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

## Co-packer memory docs

Correspondence with co-packers is tracked in one Claude Doc per co-packer.
Those docs are the memory; a session's own transcript is not, because a new
session starts without it. This applies to every session in this repo,
whatever it was opened for.

- **Before** discussing a co-packer, read its doc with the Claude Docs tools.
- **Whenever** a co-packer fact turns up (an email, a call, a quote, a
  packet, a decision about one), write it to that co-packer's doc before
  ending the turn: Terms, Open questions and next step, and a Correspondence
  log line (newest first). Facts only, each with its source; mark anything
  unconfirmed. Do this even if the session was opened for something else.
- **A co-packer with no doc yet**: create one in the same shape (How to use,
  Company facts, Terms, Open questions and next step, Correspondence log)
  and add it to the table below in the same PR as any other change, or in
  its own.
- If the Claude Docs tools are unavailable, say so and give Arthur the facts
  to paste in; don't let them live only in the chat.

The docs hold the recipe weights and quotes. They stay in Claude Docs, never
in this repo: the checkout is the public web root.

| Co-packer | Format | Memory doc |
| --- | --- | --- |
| Ibitta Enterprises | Pouch (toll) | https://claude.ai/code/artifact/830a7ccb-d9aa-47fd-bed9-dc219504abb9 |
| Co-Packing Express | Pouch | https://claude.ai/code/artifact/2928e9b4-2771-4524-a3fd-a4c666211130 |
| Qualia Provisions | Pouch | https://claude.ai/code/artifact/e88af225-7a66-4631-9cec-6c357c8de75d |
| Vanns Spices | Pouch | https://claude.ai/code/artifact/a56f661c-69b8-4f80-94d7-8961c62dc3a0 |
| Pacific Spice Company | Unknown | https://claude.ai/code/artifact/dd17e2b5-7bf8-4ee0-b4d8-17d8f78ce925 |
| The Spice Guy | Jar | https://claude.ai/code/artifact/6f17200b-d0ad-403b-8112-2f38958a8323 |
| The Spice Lab | Jar | https://claude.ai/code/artifact/2e692d62-1d48-4259-a37b-e69b68668eb8 |
| Tampico Spice | Jar | https://claude.ai/code/artifact/4bcfe71c-2dbf-4b99-bcac-d1dd542cd2b0 |
| La Criolla | Jar | https://claude.ai/code/artifact/7dd6e090-61cd-4e24-86fd-93d2623428f1 |
