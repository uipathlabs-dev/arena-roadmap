# Arena — Roadmap

Living site map / roadmap for the Arena platform, hosted on GitHub Pages with the
data stored in [`data.json`](data.json). Every save made through the web app is a
git commit, so the full change history is in this repo.

**App:** https://uipathlabs-dev.github.io/arena-roadmap/

## How it works

- `index.html` — the app (static, no build step). Renders the tree from `data.json`.
- `data.json` — the single source of truth: sections, items, statuses, and the
  per-section Purpose / Stakeholders / Target audience fields.
- Saving goes through the GitHub Contents API: the app re-reads the latest
  `data.json`, applies only your changed fields on top, and commits. Concurrent
  editors don't overwrite each other.

## Viewing

Open the app URL. No account or token needed — it's read-only by default.

## Editing (one-time setup)

1. Get **write access** to this repository (ask the owner to add you as a collaborator).
2. Create a token: GitHub → Settings → Developer settings →
   **Fine-grained personal access tokens** → Generate new token.
   - Repository access: **Only select repositories** → `arena-roadmap`
   - Permissions → Repository permissions → **Contents: Read and write**
   - Expiration: your call (90 days is fine; you can always mint a new one)
3. Open the app, click **Enable editing**, paste the token. It's stored only in
   your browser's localStorage and sent only to `api.github.com`.
4. Change statuses / fill in section fields, then hit **Save changes**.

## Statuses

| Status | Meaning |
|---|---|
| LIVE | Working today |
| IN PROGRESS | ETA end of August |
| PLANNED | Scoped, not started |
| BACKLOG | Parked for later |
| DROPPED | Out of scope |

## Editing the structure

Adding/removing sections or items = edit `data.json` directly (GitHub web editor
is fine). Each item needs a unique `id`, a `name`, a `status`, and optionally
`desc` and `children`.
