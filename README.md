# claude-marketplace (`mccavity`)

Henning Halfpap's personal **Claude Code / Codex plugin marketplace** — a single
catalog that distributes all of my plugins under one marketplace name (`mccavity`).

The plugins themselves live in their **own repositories**; this repo only hosts
the `marketplace.json` catalog and references each plugin via a `git-subdir`
source. That keeps one coherent `@mccavity` namespace while every plugin stays
independently versioned and developed.

## Hosted plugins

| Plugin | Repo | What it does |
|---|---|---|
| `paperless-bulk-plugin` | [paperless-bulk-plugin](https://github.com/McCavity/paperless-bulk-plugin) | Inbox-Triage + Bulk-Operations für Paperless-ngx |
| `iobroker-plugin` | [iobroker-plugin](https://github.com/McCavity/iobroker-plugin) | Backend-agnostische ioBroker-Diagnose-Skills |

## Install

```text
/plugin marketplace add McCavity/claude-marketplace
/plugin install paperless-bulk-plugin@mccavity
/plugin install iobroker-plugin@mccavity
```

Update the catalog after new plugins are added:

```text
/plugin marketplace update mccavity
```

## Why a dedicated marketplace repo

> **Lesson (2026-06-06):** a marketplace `name` is unique per user — *adding a
> second marketplace with the same name replaces the first*
> ([docs](https://code.claude.com/docs/en/plugin-marketplaces)). Originally each
> plugin repo self-hosted a `marketplace.json` all named `mccavity`, so adding
> one repo's marketplace silently clobbered the other's. The fix is exactly what
> the docs recommend: **one `marketplace.json`, many plugins** — here, pulled
> from their separate repos via `git-subdir`.

**Do NOT** run `/plugin marketplace add` on an individual plugin repo — add only
this hub. The plugin repos no longer carry their own `marketplace.json`.

## Adding a new plugin

Add an entry to [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json):

```json
{
  "name": "my-new-plugin",
  "source": {
    "source": "git-subdir",
    "url": "McCavity/my-new-plugin",
    "path": "plugins/my-new-plugin"
  },
  "description": "...",
  "version": "1.0.0",
  "author": { "name": "Henning Halfpap" },
  "license": "MIT",
  "tags": ["..."]
}
```

Then commit + push; users pick it up with `/plugin marketplace update mccavity`.

## License

MIT — see [LICENSE](LICENSE).
