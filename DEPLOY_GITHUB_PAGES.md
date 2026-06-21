# Getting the Ishar Map live on GitHub Pages

A complete walkthrough, from zero to a public `https://...github.io` URL. Pick
**Path A** (web upload, no tools) or **Path B** (git command line). Both end at
the same place.

Everything you upload is the **contents of this `site/` folder** — `index.html`,
`.nojekyll`, and the `maps/` folder. Do not upload the parent project; just this.

---

## Decide which kind of site you want

| Kind | Repo name | URL you get |
|------|-----------|-------------|
| **User/Org site** (recommended, cleanest URL) | must be `<username>.github.io` | `https://<username>.github.io/` |
| **Project site** | any name, e.g. `ishar-map` | `https://<username>.github.io/ishar-map/` |

If you don't already have a `<username>.github.io` repo, the user site is the
nicest. The steps below note where the two differ.

---

## Path A — Upload through the GitHub website (no git needed)

1. **Sign in** at <https://github.com>. If you don't have an account, create one
   (your username becomes part of the URL).

2. **Create the repository.**
   - Click the **+** (top right) → **New repository**.
   - **Repository name:**
     - User site → exactly `<username>.github.io` (use *your* username).
     - Project site → any name, e.g. `ishar-map`.
   - Set it to **Public**.
   - Tick **Add a README** (optional — you can delete it later).
   - Click **Create repository**.

3. **Upload the files.**
   - On the repo page click **Add file → Upload files**.
   - Open this `site/` folder on your PC, select **everything inside it**
     (`index.html`, `.nojekyll`, `README.md`, and the `maps` folder) and drag it
     into the browser. Drag the `maps` **folder** so its files keep that path.
   - If the drag doesn't include `.nojekyll` (hidden files sometimes don't drag),
     use **Add file → Create new file**, type `.nojekyll` as the name, leave it
     empty, and commit. It just needs to exist.
   - Scroll down, click **Commit changes**.

4. **Turn on Pages.**
   - Repo **Settings** (top menu) → **Pages** (left sidebar).
   - Under **Build and deployment → Source**, choose **Deploy from a branch**.
   - **Branch:** `main` (or `master`), **Folder:** `/ (root)`. Click **Save**.

5. **Wait ~1 minute**, then reload the Settings → Pages screen. It shows
   **"Your site is live at https://…"**. Click it.
   - User site → `https://<username>.github.io/`
   - Project site → `https://<username>.github.io/ishar-map/`

Done.

---

## Path B — Push with git (command line)

From inside this `site/` folder:

```bash
# one-time
git init
git add .
git commit -m "Publish Ishar map"

# create the repo on github.com first (Public), then point at it:
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

- User site → `<repo>` must be `<username>.github.io`.
- Project site → `<repo>` can be anything.

Then enable Pages exactly as in **Path A step 4** (Settings → Pages → Deploy
from a branch → `main` / `/ (root)`).

> Tip: if you'd rather keep the whole project in one repo, push the project and
> put these files in a `/docs` folder instead, then in Settings → Pages pick
> **Folder: `/docs`**. The site URL is unchanged.

---

## Updating the map later

1. In the project, re-export maps and rebuild the public whitelist.
2. Copy the fresh `index.html` and `maps/` into this folder (replace the old).
3. Re-upload (Path A: **Add file → Upload files**, drop them in, commit) or
   `git add . && git commit -m "Update map" && git push`.

GitHub Pages redeploys automatically on each commit (give it a minute). The
viewer cache-busts every request, so a hard refresh (Ctrl+F5) shows new data.

---

## Troubleshooting

- **Blank page / dropdown says "No zones.json found".** The `maps/` folder
  didn't upload with its path. Confirm the repo shows `maps/zones_public.json`
  and `maps/<zone>.json` files — not the JSON dumped into the repo root.
- **404 at the URL.** Pages can take 1–2 minutes on first publish, and the URL
  is case-sensitive. Re-check Settings → Pages shows a green "live at" banner.
- **Some files missing / weird processing.** Make sure `.nojekyll` exists in the
  root. Without it, GitHub may skip files and folders.
- **Project-site links break but user-site works.** A project site lives under a
  subpath (`/ishar-map/`). All this viewer's paths are relative (`maps/...`), so
  it handles both — just open the full URL Pages gives you, including the repo
  segment.
- **Changes don't show.** Hard refresh (Ctrl+F5). If still stale, confirm the
  commit actually landed on the branch Pages is serving.

---

## Optional: custom domain

Settings → Pages → **Custom domain**, enter e.g. `map.yourdomain.com`, then at
your DNS provider add a **CNAME** record pointing that name to
`<username>.github.io`. Tick **Enforce HTTPS** once it validates. GitHub writes a
`CNAME` file into the repo — leave it there.
