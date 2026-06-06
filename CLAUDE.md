# claude-marketplace — Conventions for AI agents

> Last update: 2026-06-06

This repo is a **plugin marketplace catalog only** — the `mccavity` marketplace.
It contains no plugin code. Each listed plugin lives in its own repository and is
referenced from `.claude-plugin/marketplace.json` via a `git-subdir` source.

## Why this repo exists

A Claude Code marketplace `name` is **unique per user**: adding a second
marketplace with the same name *replaces* the first
([docs](https://code.claude.com/docs/en/plugin-marketplaces)). Earlier, each
plugin repo (`paperless-bulk-plugin`, `iobroker-plugin`) self-hosted a
`marketplace.json` all named `mccavity` — so adding one clobbered the other
(observed 2026-06-06). This hub is the documented fix: **one `marketplace.json`,
many plugins**, each pulled from its own repo.

## Rules

- **Catalog only.** No `plugins/` directory here, no skills, no MCP. Just
  `.claude-plugin/marketplace.json` + docs.
- **One marketplace name (`mccavity`).** Never create another marketplace named
  `mccavity` anywhere. The plugin repos must NOT carry their own
  `marketplace.json` (removed 2026-06-06) — otherwise adding a plugin repo as a
  marketplace re-introduces the collision.
- **git-subdir sources.** Each plugin lives at `plugins/<name>/` inside its repo,
  so the source is `{ "source": "git-subdir", "url": "McCavity/<repo>", "path": "plugins/<name>" }`.
  Optionally pin with `ref`/`sha` for reproducibility.
- **Keep versions in sync.** The `version` in each catalog entry should match the
  plugin's own `plugin.json` version. Bump here when the plugin bumps.
- Solo-maintainer repo: branch protection with `required_approving_review_count: 0`,
  `enforce_admins: false`. PR-based for changes; initial scaffold is one commit on `main`.
