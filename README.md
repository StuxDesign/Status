<p align="center">
  <picture><source media="(prefers-color-scheme: dark)" srcset="https://global.media.stux.design/logo-light.png"><source media="(prefers-color-scheme: light)" srcset="https://global.media.stux.design/logo-dark.png"><img src="https://global.media.stux.design/logo-dark.png" height="100" alt="Stux.Design Logo"></picture>
</p>

# Status

### *Live status of Stux.Design's sites, powered by [GitHup](https://githup.stux.group).*

**Status page:** [status.stux.design](https://status.stux.design)

<!-- A live badge: reads the overall status straight from data/summary.json. -->
[![Stux.Design status](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2FStuxDesign%2FStatus%2Fmain%2Fdata%2Fsummary.json&query=%24.status&label=status&style=for-the-badge)](https://status.stux.design)

## Current status

Updated by GitHup whenever the status page is rebuilt (hourly, and when a status changes).

<!-- githup:start -->
<!-- This table is written by GitHup (https://github.com/StuxGroup/GitHup); edits here are overwritten. -->

**All systems operational** · [Live status page](https://status.stux.design/)

| Group | Monitor | Status | Uptime (24 h) | Uptime (7 d) | Uptime (30 d) | Response time (24 h) |
| ----- | ------- | ------ | ------------- | ------------ | ------------- | -------------------- |
| Stux.Design | [Stux.Design Website](https://stux.design/) | Up | 100.00% | 100.00% | 100.00% | 506 ms |
| Shared | [Stux.Design Media CDN](https://global.media.stux.design/icon.png) | Up | 100.00% | 100.00% | 100.00% | 498 ms |
<!-- githup:end -->

## What's monitored

Every 5 minutes (when GitHub runs the schedule late, a run checks up to 4 times, 5 minutes apart, to fill the gap), GitHup checks each monitor in [`.githup.yml`](.githup.yml):

- **Stux.Design:** the Stux.Design website
- **Shared:** the Stux.Design media CDN
- **On the drawing board:** Stux.Design Services, soonpage, maintenancepage and servicepage are
  listed as plain links, not checked, because they don't serve yet. Move each into the
  Stux.Design group as a monitor once it's live

To add a site, add a monitor to the right group there (or a new group). A group can also hold `links:` instead of monitors, for sites that should be listed but not checked.

When a site goes down, GitHup opens an Issue on this repository (labelled `githup`,
`incident`, `status` and the monitor's slug) and closes it with the downtime when it recovers.
To announce planned maintenance, open an Issue yourself with the `githup` and `incident` labels
(plus the monitor's slug to link it); it shows on the status page.

## How it works

- **`.github/workflows/status.yml`** runs a GitHup `check` every 5 minutes (with `fill-gaps`, up to 4 checks when the schedule is late) and commits the
  results to `data/` as `github-actions[bot]`. When a status changes, hourly, and on pushes, it
  builds the GitHup status page into `_site` (with `site-dir`), and deploys it with `actions/deploy-pages`.
- **`legal:` in `.githup.yml`** makes GitHup generate the **Boring Legal Stuff** hub at `/legal/`
  with its six sub-pages, a themed `404.html`, a `/sitemap/` page, `sitemap.xml` and `robots.txt`
  (the base URL is `site.url`). Nothing is hand-made, and the footer shows only
  **Powered by GitHup**. This repo's own `CHANGELOG.md` and `VERSION.md` are for this repo only.
- **`data/`** is the monitoring history, created by the first check. Don't edit it by hand.
- **The status table above** is written by GitHup's `readme` mode between the
  `<!-- githup:start -->` and `<!-- githup:end -->` markers. Don't edit inside them.

## Local development

```bash
./dev-server.sh                 # or dev-server.bat on Windows; add a port as the last argument
./dev-server.sh --no-dev-mode   # production rendering
```

`dev-server` generates 90 days of example data, builds the status page into `.dev/public` with
`DEV_MODE` on, with its legal pages, 404 and sitemap, and serves it at
`http://127.0.0.1:8000`. It uses GitHup from `$GITHUP_PATH`, a sibling `../GitHup` checkout, or
a fresh clone in `.dev/GitHup`.

## Hosting

GitHub Pages, deployed by Actions (**Settings → Pages → Source: GitHub Actions**), with the custom
domain `status.stux.design` set in the Pages settings. DNS: a `CNAME` record for `status` pointing
at `stuxdesign.github.io`. The repository is public, so the page's live refresh can read
`data/summary.json` straight from GitHub.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

&copy; 2026 Stux.Group. All rights reserved. This repository is not licensed for reuse or
redistribution, see [LICENSE](LICENSE).

---

*Designed with purpose. | Part of the Stux.Group Brand of Companies.*

*Built & Maintained by <picture><source media="(prefers-color-scheme: dark)" srcset="https://global.media.stux.design/icon-light.png"><source media="(prefers-color-scheme: light)" srcset="https://global.media.stux.design/icon-dark.png"><img src="https://global.media.stux.design/icon-dark.png" height="14" alt="Stux.Design" valign="middle"></picture> [Stux.Design](https://github.com/StuxDesign), powered by [GitHup](https://githup.stux.group).*
