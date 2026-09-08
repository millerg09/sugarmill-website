# Sugar Mill Music

Single-page site for Sugar Mill Music, a home recording studio in Manhattan.
Plain HTML/CSS, no build step, hosted free on GitHub Pages at
[sugarmillmusic.com](https://sugarmillmusic.com).

## Working on it locally

There's no build step. Open `index.html` directly in a browser to preview,
or run a tiny local server if you want relative paths to behave exactly
like production:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

## What's still placeholder

- **Copy** — hero tagline, about paragraph, services list, contact intro.
  Marked with `<!-- PLACEHOLDER COPY -->` comments in `index.html`.
- **Images** — `images/` holds the real photos once you have them. Swap the
  two `.placeholder-box` divs (recording desk, headshot) in `index.html`
  for `<img src="images/your-file.jpg" alt="...">`.
- **Social links** — `href="#"` placeholders in the contact section; drop
  in real profile URLs once accounts exist.
- **Email** — shown as plain text (`sugarmillmusic at gmail dot com`) to
  keep it off scraper radars. No link, no JS needed.

## Deployment workflow

The site is a static GitHub Pages site served from `main`. Updates are a
plain edit-commit-push cycle — GitHub redeploys automatically in under a
minute, and every version is preserved in git history, so a bad change is
always one `git revert` away.

```
# edit files locally, then:
git add .
git commit -m "describe the change"
git push
```

That's it — no staging environment, no separate build. If you want to
preview a bigger change before it's live, make the edits on a branch, view
it locally, then merge to `main` when it looks right.

## One-time setup (do this once)

### 1. Create the GitHub repo

1. On GitHub, create a new **public** repository (Pages' free tier
   requires public for personal accounts).
2. From this folder:
   ```
   git init
   git add .
   git commit -m "Initial site scaffold"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```

### 2. Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set source to **Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
3. Under **Custom domain**, enter `sugarmillmusic.com` and save. (This repo
   already includes a `CNAME` file with that domain, so GitHub should pick
   it up automatically — the settings field just confirms it.)

### 3. Point the domain at GitHub (in GoDaddy DNS)

In GoDaddy's DNS management for `sugarmillmusic.com`:

| Type  | Name | Value                     |
|-------|------|---------------------------|
| A     | @    | 185.199.108.153           |
| A     | @    | 185.199.109.153           |
| A     | @    | 185.199.110.153           |
| A     | @    | 185.199.111.153           |
| CNAME | www  | `<your-username>.github.io.` |

Remove any default GoDaddy parking A/CNAME records first — they'll
conflict. DNS changes can take anywhere from a few minutes to ~48 hours
to propagate.

### 4. Enforce HTTPS

Once DNS has propagated, back in **Settings → Pages**, check
**Enforce HTTPS** as soon as it's selectable. GitHub issues the SSL
certificate automatically — no cert management needed going forward.
