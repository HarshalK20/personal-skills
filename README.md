# Personal Skills Marketplace

A dual-compatible plugin marketplace for **Cursor** and **Claude Code**. Contains personal productivity plugins for AI-assisted workflows.

## Plugins

| Plugin | Description |
|---|---|
| [job-search-toolkit](plugins/job-search-toolkit/) | Resume tailoring, company research, interview prep, salary intelligence, and negotiation strategies for senior engineering leadership roles |
| [finance-toolkit](plugins/finance-toolkit/) | Portfolio analysis, rebalancing alerts, tax-loss harvesting, and market intelligence using Zerodha Kite |

## Installation

### Cursor

Add this repository as a marketplace source, or symlink individual plugins to `~/.cursor/plugins/local/`:

```bash
ln -s /path/to/personal-skills/plugins/job-search-toolkit ~/.cursor/plugins/local/job-search-toolkit
```

### Claude Code

Add as a marketplace and install plugins:

```bash
/plugin marketplace add /path/to/personal-skills
/plugin install job-search-toolkit@personal-skills
```

Or use a plugin directly for a session:

```bash
claude --plugin-dir /path/to/personal-skills/plugins/job-search-toolkit
```

## Structure

```
personal-skills/
├── .cursor-plugin/marketplace.json    # Cursor marketplace registry
├── .claude-plugin/marketplace.json    # Claude Code marketplace registry
├── plugins/
│   ├── job-search-toolkit/            # Job search skills
│   │   ├── .cursor-plugin/plugin.json
│   │   ├── .claude-plugin/plugin.json
│   │   ├── skills/                    # Shared skills (both tools)
│   │   ├── rules/                     # Cursor rules
│   │   └── templates/                 # Reference templates
│   └── finance-toolkit/              # Finance skills
│       ├── .cursor-plugin/plugin.json
│       ├── .claude-plugin/plugin.json
│       ├── skills/                    # Shared skills (both tools)
│       ├── mcp.json / .mcp.json       # Kite MCP server config
└── .gitignore
```

## Adding New Plugins

1. Create a new directory under `plugins/<plugin-name>/`
2. Add both `.cursor-plugin/plugin.json` and `.claude-plugin/plugin.json`
3. Add skills, commands, agents, hooks as needed
4. Register the plugin in both marketplace files at the root
