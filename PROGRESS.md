# Progress Log

Running record of where this project stands, so a new session can pick up
without re-deriving context. Update this when a work session ends.

## Status as of 2026-09-08

**The site is live at [sugarmillmusic.net](https://sugarmillmusic.net).**
GitHub Pages domain check passed, SSL certificate issued, and "Enforce
HTTPS" was just checked in Settings → Pages. HTTP → HTTPS redirect hadn't
kicked in yet as of the last check (`curl -I http://sugarmillmusic.net`
was still returning `200` instead of a `301` redirect) — worth a quick
recheck next session; it's a propagation-speed thing, not a
misconfiguration.

## What's done

- Repo: [github.com/millerg09/sugarmill-website](https://github.com/millerg09/sugarmill-website) (public)
- Domain `sugarmillmusic.net` registered via **Wix** (not GoDaddy — the
  original `sugarmillmusic.com` was never actually owned; Wix's DNS panel
  is what's documented in the README, not GoDaddy's)
- DNS pointed at GitHub Pages, HTTPS certificate issued
- Hero, About, and Services copy finalized
- Spotify playlist embedded (`60M1ZSzD8sR0UXUZUx6p9F`)
- Desk and headshot photos in place as placeholders
- Instagram linked (`instagram.com/sugarmillmusic`)
- Email shown as scraper-resistant plain text
- Git push workflow working end-to-end (credential cached in macOS Keychain)

## Open follow-ups (not urgent, whenever you get to it)

1. **Confirm the HTTPS redirect took effect** — `curl -I http://sugarmillmusic.net`
   should show a `301` to `https://`. If not yet, just wait a bit longer.
2. **Real photos** — current desk/headshot images are placeholders; swap
   in `images/sugarmill_desk.jpg` and `images/sugarmill_headshot.jpg` once
   better ones exist (same filenames = no code changes needed).
3. **Contact intro line** — still placeholder copy ("Have a song you want
   to record? Reach out and let's talk.") in the `#contact` section of
   `index.html`. Workshop final wording whenever.
4. **More social links** — only Instagram exists so far; add others to the
   `.social-links` div in `index.html` as accounts are created.
5. **Pricing/rates** — not addressed yet; decide if/how to publish them.
6. **Optional cleanup** — the GitHub personal access token used to set up
   `git push` was pasted into a chat session. It's scoped to `repo` only
   and expires ~90 days from 2026-09-08, so there's no urgency, but you
   can revoke and regenerate it anytime for peace of mind (GitHub →
   Settings → Developer settings → Personal access tokens).
