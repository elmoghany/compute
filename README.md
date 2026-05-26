# cloudcompute — web dashboard

The static web dashboard for [cloudcompute](https://github.com/elmoghany/cloudcompute),
a private, self-hosted compute node that runs on your own PC.

**Live:** https://elmoghany.github.io/compute/

## How it works

GitHub Pages can only serve static files, so this repo is **just the UI** — a single
`index.html`. It does not contain the node, your credentials, or any secrets.

When you open it, you enter your node's **public API URL** (the address of the
tunnel exposing your PC, e.g. `https://xxxx.lhr.life`) plus your username/password.
The page then talks directly to your node's API from your browser:

```
browser (elmoghany.github.io/compute)  ──HTTPS──▶  public tunnel  ──▶  cloudcompute on your PC
```

- The API URL is stored in your browser's `localStorage`; update it whenever you
  restart the tunnel (anonymous tunnel URLs change each time).
- Your node must allow this origin via CORS (it does by default; configurable with
  `CC_CORS_ORIGINS`).
- Auth uses bearer tokens, so nothing is cookie-bound and the static origin can't
  silently act on your behalf.

The backend, authentication, and command-execution logic live in the **private**
`cloudcompute` repo. This public repo is only the front-end so GitHub Pages can host it.

> ⚠️ A reachable node runs commands on your PC for any authenticated user. Use a
> strong password and stop the tunnel when you're not using it.
