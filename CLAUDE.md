# AxisPrime Website

## Workflow
- Repo: `C:\Users\barnh\OneDrive\Software Development\AxisPrime Website` (inside OneDrive).
- Branch: `main` (only branch; tracks `origin/main`).
- Remote: GitHub `barnhartanthony2448/AxisPrime-Website` (`origin`).
- Pushing does NOT deploy. The Netlify site is not git-connected; GitHub is version history only. Deploy is a separate manual step (see Infrastructure & deploy).

### Test locally first
- After a change, don't commit or push yet. Run it locally, tell me exactly what to open and what to check, and wait.
- Commit and push only after I say it works locally. A push may deploy to production, so never push in order to test.
- If a local run would touch production data or real services (production database, live payments, real emails or messages), tell me and get my OK first.
- Docs, pipeline and server config changes also wait for my OK before committing.
- Run it locally by opening `index.html` in a browser. Pushing to GitHub doesn't deploy; going live is a separate `netlify deploy --prod`, which also waits for my OK.

## What it is
Company marketing site for AxisPrime, Inc. (workforce management for sporting events, arenas, stadiums, race tracks and special events), live at axisprimeinc.com. One page with sections: nav, `#hero`, `#about`, `#snodo`, `#solutions`, `#why`, `#contact`, footer.

## Stack
- Single static `index.html` (~1,400 lines) with inline `<style>` and inline `<script>`. No framework, no package.json, no build step.
- Fonts: Google Fonts (Barlow Condensed, Inter) loaded via `<link>`.
- Inline JS: hero `<canvas>` animation, scroll-reveal via IntersectionObserver, contact form handler.
- Hosting: Netlify. DNS: GoDaddy.

## Running locally
- Open `index.html` directly in a browser, or serve the folder with any static server. TODO: confirm preferred local server/command.
- Needs internet for Google Fonts; everything else is local.

## Infrastructure & deploy
- Netlify site `axisprime-website` (default URL `axisprime-website.netlify.app`), linked locally via `.netlify/state.json` (holds the site ID; do not copy it anywhere).
- Deploy manually from the project root: `netlify deploy --prod --dir .`
- Requires the globally installed, already-authenticated `netlify-cli`.
- Custom domain `axisprimeinc.com` registered at GoDaddy; DNS records at GoDaddy point `@` and `www` to Netlify. SSL is auto-provisioned by Netlify.
- Auto-deploy on push was intentionally not set up. Enabling it would mean linking the repo in the Netlify dashboard; only do that if asked.

## Key directories
- `index.html`: the entire site (markup, CSS, JS).
- `assets/`: images referenced by the page: `logo-lockup.png` (nav + footer), `logo-full.png` (hero banner).
- `AxisPrime Logo Choices/`: untracked logo drafts; not referenced by the page.
- `.netlify/`: local Netlify CLI link/state; gitignored.
- `.gitignore`: currently untracked; ignores `.netlify`.

## Conventions & gotchas
- Theme colors and fonts are CSS custom properties on `:root` (e.g. `--red: #E4051A`, `--bg`, `--font-head`, `--font-body`). Reuse them; don't hard-code new colors.
- Single responsive breakpoint at `@media (max-width: 900px)`.
- The contact form does not send anything: `handleSubmit()` only calls `preventDefault()`, shows "Message Sent" for 3 seconds, then resets. TODO: confirm whether a real submission backend (e.g. Netlify Forms) is wanted.
- `netlify deploy --dir .` publishes the whole folder, so `AxisPrime Logo Choices/` (and `CLAUDE.md`) likely get uploaded too. TODO: confirm what Netlify CLI excludes and whether to deploy from a cleaner directory.
- Logo images were recently re-cropped to avoid cutting off the flag/underline; check nav and footer rendering after any logo change.
- TODO: confirm whether `.gitignore` and `AxisPrime Logo Choices/` should be committed or left untracked.

## Versions
Version rules: see "Versions" in `~/.claude/CLAUDE.md`. Live = "<name> v<N>"; a major update being built locally = "<name> α".
- Display name: **AxisPrime**
- Live: AxisPrime v1 (tag `v1` on `main` = `0f82c42`; the live site matched this commit on 2026-11-11)
- In progress: none
- Shown in the app: not yet. Offer to add it (read from one place in the code) the first time we work on it.

### History
- 2026-11-11: v1. Starting point: the commit live at setup.
