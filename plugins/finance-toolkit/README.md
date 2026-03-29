# Finance Toolkit

A dual-compatible plugin (Cursor + Claude Code) for personal finance intelligence. Fetches live portfolio data from Zerodha Kite and generates actionable reports with exit alerts, rebalancing suggestions, tax-loss harvesting opportunities, and market context.

## Skills

| Skill | Trigger | What It Does |
|---|---|---|
| `portfolio-analyzer` | "Analyze my portfolio" | Fetches holdings, positions, and MF data from Kite; computes P&L, flags instruments needing attention; deep-dives on flagged ones; generates a structured report |

## Trigger Phrases

- "Analyze my portfolio"
- "Portfolio health check"
- "Should I sell any stocks?"
- "Which stocks are in loss?"
- "Review my mutual funds"
- "Any tax loss harvesting opportunities?"
- "Am I too concentrated in IT?"
- "What's the early warning in my holdings?"

## Prerequisites

This plugin requires the **Zerodha Kite MCP server** to fetch live portfolio data. The plugin includes `mcp.json` / `.mcp.json` configs that auto-start the server.

Make sure you have Node.js installed (for `npx`). If your Kite MCP server uses a different command or needs environment variables (e.g. API key, secret), update the MCP config files accordingly:

- `mcp.json` -- used by Cursor
- `.mcp.json` -- used by Claude Code

## Install in Cursor

```bash
ln -s "$(pwd)" ~/.cursor/plugins/local/finance-toolkit
```

## Install in Claude Code

```bash
# Option A: Direct plugin directory
claude --plugin-dir ./plugins/finance-toolkit/

# Option B: Via marketplace
# /plugin marketplace add /path/to/personal-skills
# /plugin install finance-toolkit@personal-skills
```

## Report Sections

The portfolio analyzer generates a structured markdown report with:

1. **Portfolio Snapshot** -- total invested, current value, P&L across stocks and mutual funds
2. **Priority Alerts** -- exit/stop-loss alerts, rebalancing triggers, tax-loss harvesting candidates
3. **Health Check** -- every holding with full financial details and signal (HOLD/WATCH/REDUCE/EXIT)
4. **Sector Allocation** -- concentration analysis with risk levels
5. **Strategic Recommendations** -- prioritized action list ordered by urgency
6. **Market Context** -- Nifty, FII/DII activity, RBI rate, sector outlook relevant to your holdings
