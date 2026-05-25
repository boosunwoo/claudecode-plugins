# claudecode-plugins

A small, curated marketplace of [Claude Code](https://docs.claude.com/en/docs/claude-code) plugins by [@boosunwoo](https://github.com/boosunwoo).

## Quick install

In any Claude Code session:

```
/plugin marketplace add github.com/boosunwoo/claudecode-plugins
/plugin install <plugin-name>
```

That's it. The marketplace registers, and you can browse and install any plugin listed below with a single command.

## Available plugins

| Plugin | What it does | Install |
|---|---|---|
| [`session-tracker`](https://github.com/boosunwoo/session-tracker) | Saves each Claude Code session as a browseable markdown record in `~/claude-sessions/` with title, summary, key decisions, modified files, and a `claude --resume` command. Auto-saves on exit; refine manually via `/session-tracker`. | `/plugin install session-tracker` |

More plugins coming as I build them. PRs welcome.

## How this works

This repo is a **Claude Code marketplace** — a manifest (`.claude-plugin/marketplace.json`) that points to individual plugin repos. The plugins themselves live in their own repositories so they can be developed and versioned independently.

```
claudecode-plugins/                         (this repo — marketplace manifest)
└── .claude-plugin/
    └── marketplace.json
        ↓ references
boosunwoo/session-tracker                   (separate repo — actual plugin code)
├── .claude-plugin/plugin.json
├── skills/session-tracker/
└── hooks/hooks.json
```

When you run `/plugin install session-tracker`, Claude Code reads this marketplace's manifest, finds the plugin's source URL and pinned commit SHA, fetches it, and installs locally.

## Contributing a plugin

If you've built a Claude Code plugin and want it listed here:

1. Host your plugin in its own public GitHub repo.
2. Make sure it has the required structure: `.claude-plugin/plugin.json` + `skills/`, `commands/`, `agents/`, or `hooks/`.
3. Open a PR to this repo adding an entry to the `plugins` array in `.claude-plugin/marketplace.json`:

```json
{
  "name": "your-plugin",
  "description": "What it does, one sentence.",
  "author": { "name": "your-handle" },
  "category": "productivity|development|...",
  "source": {
    "source": "git",
    "url": "https://github.com/you/your-plugin.git",
    "ref": "v0.1.0",
    "sha": "<commit-sha-of-the-ref>"
  },
  "homepage": "https://github.com/you/your-plugin"
}
```

## License

MIT — see [LICENSE](./LICENSE). Plugins listed here retain their own licenses.
