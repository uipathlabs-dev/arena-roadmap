# Arena — Roadmap

Living site map / roadmap for the Arena platform, hosted on GitHub Pages with the
data stored in [`data.json`](data.json). Every save made through the web app is a
git commit, so the full change history is in this repo.

**App:** https://uipathlabs-dev.github.io/arena-roadmap/

## How it works

- `index.html` — the app (static, no build step). Renders the tree from `data.json`.
- `data.json` — the single source of truth: sections, items, statuses, and the
  per-section Purpose / Stakeholders / Target audience fields.
- Saving goes through the GitHub Contents API: right before writing, the app
  re-reads `data.json` and checks whether it still matches what you loaded. If
  someone else saved in the meantime, you're asked whether to overwrite (their
  version stays recoverable from git history regardless). Otherwise it writes
  your full edited tree as a new commit.

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
4. Edit inline, then hit **Save changes**.

## What you can edit in the app

- **Add a section** — the dashed "+ Add section" button at the bottom of the page.
  Click into its title to rename it, and fill in Section purpose / Stakeholders /
  Target audience directly in their boxes.
- **Delete a section** — "delete section" button in its header (confirms first;
  removes all its items too).
- **Add an item** — "+ Add item" under a section adds a top-level item there;
  "+ sub" on any item adds a nested sub-item under it (any depth).
- **Edit an item** — click its name or description to type directly; change its
  status from the dropdown.
- **Delete an item** — "delete" button on the item (confirms first; removes its
  sub-items too).

Newly added or edited items/sections get a small **new** / **edited** badge and
an accent stripe until you save. The toolbar shows a live count (e.g. "2 added,
1 edited") and the **Save changes** button is disabled until there's something
to save.

## Statuses

| Status | Meaning |
|---|---|
| LIVE | Working today |
| IN PROGRESS | ETA end of August |
| PLANNED | Scoped, not started |
| BACKLOG | Parked for later |
| DROPPED | Out of scope |

## Editing `data.json` directly

For bulk changes, editing the file in the GitHub web editor works too — the app
just reads whatever is there on next load. Each item needs a unique `id`, a
`name`, a `status`, and optionally `desc` and `children` (an array of items,
same shape, for nesting).
