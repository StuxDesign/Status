<p align="center">
  <picture><source media="(prefers-color-scheme: dark)" srcset="https://global.media.stux.design/logo-light.png"><source media="(prefers-color-scheme: light)" srcset="https://global.media.stux.design/logo-dark.png"><img src="https://global.media.stux.design/logo-dark.png" height="80" alt="Stux.Design Logo"></picture>
</p>

# Contributing to Stux.Design Status

Stux.Design Status is Stux.Design's status page, [status.stux.design](https://status.stux.design), built with
[GitHup](https://githup.stux.group). To report an outage, open an Issue. Bugs or ideas for the
status page software belong in [StuxGroup/GitHup](https://github.com/StuxGroup/GitHup/issues).

## Local setup

You need Python 3.11+ and nothing else.

```bash
./dev-server.sh [--no-dev-mode] [--lan] [port]   # or dev-server.bat on Windows
```

`--lan` listens on all interfaces instead of 127.0.0.1 only, so a phone or tablet on the same
network can open it, and prints the addresses to use.

## Project conventions

- **Monitors live in `.githup.yml`.** Its syntax is documented in the
  [GitHup docs](https://githup.stux.group/docs/). Only add sites Stux.Design runs.
- **The status page itself is GitHup's**, including the legal pages and 404. Change how it
  looks or works in GitHup, not here.
- **Brand.** The Stux.Design accent is `#e71081`, set as `site.accent`. The logo and favicon are the Stux.Design
  Status badge icon, served from services.stux.design (built by `scripts/badge-icons.py` in `StuxDesign/Services`).
- **Legal pages.** The `legal:` block in `.githup.yml` drives **Boring Legal Stuff** at `/legal/`.
  Keep it accurate.
- **Don't edit `data/` by hand.** It belongs to GitHup and the workflow.

## Branches and going live

- **`main` is what's live.** Nothing is pushed to it directly: it only changes when a pull request from `staging` is merged. Merging into `main` rebuilds the status page. The status workflow commits monitoring data straight to `main`, so `main` runs ahead of `staging` and `test`: merge `main` back into both when they drift.
- **`staging` is the last check before live.** It only changes when a pull request from `test` is merged. There's no separate staging site, so checking it means CI plus a look at the branch locally.
- **Work happens on `test`**, or on a feature branch off `test` that's merged back into it. Releases are made on `test` too; `commit.sh` / `commit.bat` refuse to run on `staging` or `main`.
- **Going live:** push `test` with its tag (`git push origin test --tags`), open a pull request into staging (`gh pr create --base staging --head test`), check staging once it's merged, then open one from staging into main (`gh pr create --base main --head staging`). Both pull requests need CI to pass and are reviewed and merged by Leo.

## Versioning

This project uses [Date Versioning](https://datevers.ing). To release:

1. Add a `## vYY.MM.DD` entry at the top of `CHANGELOG.md`, with its sections in this order: Added, Changed, Fixed, Removed, Security, Deprecated.
2. Set `VERSION.md` to the same bare version (no `v`): today's **UTC** date as `YY.MM.DD`, or `YY.MM.DD-1`, `-2`… for later releases the same UTC day. Never a future date. Use UTC, not local time: just after midnight in the UK it is still the previous day in UTC.
3. Run `bash tests/version.sh`.
4. Run `./commit.sh` (or `commit.bat` on Windows). It checks the version, commits and tags `vYY.MM.DD`, and never pushes.
