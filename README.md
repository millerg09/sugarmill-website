# Sugar Mill Music

Single-page site for Sugar Mill Music, a home recording studio in Manhattan.
Plain HTML/CSS, no build step, hosted free on GitHub Pages at
[sugarmillmusic.net](https://sugarmillmusic.net) — **live as of 2026-09-08.**

See [PROGRESS.md](PROGRESS.md) for current status and open follow-ups.

## Working on it locally

There's no build step. Open `index.html` directly in a browser to preview,
or run a tiny local server if you want relative paths to behave exactly
like production:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

## What's still placeholder

- **Contact intro line** — the one remaining `<!-- PLACEHOLDER COPY -->`
  comment in `index.html`, in the `#contact` section.
- **Photos** — `images/sugarmill_desk.jpg` and `images/sugarmill_headshot.jpg`
  are real files, but placeholder-quality. Drop in better ones under the
  same filenames whenever they're ready — no code changes needed.
- **Social links** — only Instagram is linked so far. Add more `<a>` tags
  to `.social-links` in `index.html` as other accounts exist.

Email is intentionally final as-is: shown as plain text
(`sugarmillmusic at gmail dot com`) to keep it off scraper radars, no
link or JS needed.

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

## One-time setup (already done — kept for reference)

This has already been completed for this repo/domain. Kept here in case
the site is ever migrated to a new repo, domain, or GitHub account.

### 1. Create the GitHub repo

1. On GitHub (account `millerg09`), create a new **public** repository
   (Pages' free tier requires public for personal accounts). This folder
   is already a git repo with an initial commit, so no `git init` needed.
2. From this folder:
   ```
   git branch -M main
   git remote add origin https://github.com/millerg09/<repo-name>.git
   git push -u origin main
   ```

### 2. Turn on GitHub Pages

1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set source to **Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
3. Under **Custom domain**, enter `sugarmillmusic.net` and save. (This repo
   already includes a `CNAME` file with that domain, so GitHub should pick
   it up automatically — the settings field just confirms it.)

### 3. Point the domain at GitHub (in Wix DNS)

The domain is registered through Wix, not GoDaddy — Wix lets you edit DNS
records directly without changing nameservers, which is actually simpler
than the GoDaddy path in the original plan.

1. In Wix, go to **Domains**, click the **Domain Actions** icon next to
   `sugarmillmusic.net`, and choose **Manage DNS Records**.
2. **Delete Wix's default A and CNAME records first** — Wix auto-creates
   records pointing at Wix hosting when you register a domain, and they'll
   conflict with the ones below.
3. Add these records:

   | Record type | Host Name       | Value                    |
   |--------------|-----------------|--------------------------|
   | A            | *(leave blank — represents `@`/root)* | 185.199.108.153 |
   | A            | *(leave blank)* | 185.199.109.153          |
   | A            | *(leave blank)* | 185.199.110.153          |
   | A            | *(leave blank)* | 185.199.111.153          |
   | CNAME        | www             | `millerg09.github.io`    |

Wix's "Host Name" field represents the root domain by being left empty,
not by typing `@` — typing `@` literally will create the wrong record.
DNS changes can take anywhere from a few minutes to ~48 hours to
propagate.

### 4. Enforce HTTPS

Once DNS has propagated, back in **Settings → Pages**, check
**Enforce HTTPS** as soon as it's selectable. GitHub issues the SSL
certificate automatically — no cert management needed going forward.
