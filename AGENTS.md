# Windward Strategy — operating contract

Operating contract for AI work in this repo; the global `~/AGENTS.md` still applies. The advisory division chart room — operations and technology by engagement. Live at strategy.windwardline.com. Zero-dependency static HTML.

## Commands

Preview: `python3 -m http.server 8907` (mirrors the untracked `.claude/launch.json`). CI-equivalent: `npx --yes html-validate@9 index.html` · JSON-parse `vercel.json`.

## Gates

CI is html-validate on `index.html` plus the `vercel.json` parse. `schedule.html` and `script.js` are not checked. Push to main deploys production. A parallel `security.yml` (PRs, pushes, weekly cron) gates Semgrep and secret scan; a post-deploy job asserts the production security headers. An advisory Claude review runs on every same-repo PR via `claude-review.yml`, which deliberately calls the fleet reusable at `@main` — one merge updates every repo. It activates only when the `ANTHROPIC_API_KEY` secret is present; fork PRs never receive secrets, so they skip it by security design.

## Laws

- Koalendar slug `windward-strategy` is hardcoded in `schedule.html`; CSP `frame-src https://koalendar.com` in `vercel.json`; change both together.
- The `/schedule` copy is deliberately different from the other divisions — "Forty-five minutes" and "Take the pilot aboard." where the siblings say thirty and "Book a call." Do not normalize it.
- The Golf flag ("I require a pilot") is six alternating bars with hardcoded fills (`#c9a25e` / `#202e4d`) repeated across six `<rect>` elements in both HTML files; only `--gf-stroke` is themed.
- Four `:root` blocks — an accent change touches all four. Never commit `.env.local` (`vercel link` drops an OIDC token there).
- `cleanUrls: true` maps `/schedule` → `schedule.html`. `.vercelignore` excludes `docs/`.
