# Ishar Map — Static Site

Self-contained, read-only map viewer. Pure static files — no server, no build
step. Just upload and serve.

## Contents

```
index.html              The read-only public map viewer
.nojekyll               Disables GitHub Pages' Jekyll processing (leave it in)
maps/
  zones_public.json     Dropdown whitelist (the published zones)
  <zone>.json           One file per published zone
```

Only published zones are included. Fonts load from the Google Fonts CDN; all
icons and styles are inline, so nothing else is needed.

## Publish on GitHub Pages

Upload the **contents of this folder** (not the folder itself) to your Pages repo:

- **User/org site** (`<you>.github.io` repo): put the contents in the repo root.
- **Project site**: put the contents either in the repo root of a `gh-pages`
  branch, or in a `/docs` folder, then set
  **Settings → Pages → Source** to that branch/folder.

Pages will serve `index.html` automatically. Give it a minute after the first
push, then load `https://<you>.github.io/` (or `.../<repo>/` for a project site).

## Updating later

Regenerate in the project, then recopy:

1. Re-export the maps and rebuild the public whitelist.
2. Replace `index.html` and the `maps/` folder here with the fresh versions.
3. Commit and push — Pages redeploys on push.

The viewer cache-busts every fetch, so a hard refresh shows new data immediately.

## Local preview

```
python -m http.server 8000
```

then open <http://127.0.0.1:8000/>. (Opening `index.html` directly with a
`file://` URL won't work — browsers block the `maps/*.json` fetches without a
server.)
