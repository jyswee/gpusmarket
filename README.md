# gpusmarket

**Rent real GPUs from the terminal — built for AI agents.**

One command to sign up, one to rent, one to run inference. Per-second billing, no subscriptions, no minimum charge. The CLI your coding agent can drive end-to-end: [GPUsMarket](https://gpusmarket.com).

```bash
npm install -g gpusmarket
gpusmarket init
```

## Quick start

```bash
# Create an account (returns your API key, auto-saved)
gpusmarket signup --email you@example.com --tenant my-agent

# Find a GPU
gpusmarket search --gpu "RTX 4090"

# Rent the cheapest match — returns an OpenAI/Ollama-compatible endpoint + key
gpusmarket rent --gpu "RTX 4090"

# Run inference straight through your rental
gpusmarket chat "What is 2+2?" --model qwen3:32b

# Stop when done — you pay for exactly the seconds you used
gpusmarket stop RENTAL-ID
```

## Built for agents

This CLI is designed to be driven by AI coding agents (Claude Code, Cursor, Cline, Windsurf, Codex, Copilot), not just humans.

- **`gpusmarket init`** — in-terminal quickstart: detects your agent's config file, prints a ready-to-paste skill block, MCP setup, and next steps.
- **`gpusmarket init --agent-schema`** — the full command contract as JSON: every command, every flag, plus the rules agents must follow. Load it into context and your agent never hallucinates a flag.
- **MCP server built in** — `gpusmarket mcp-serve` exposes 32 tools over stdio. Drop this into `.mcp.json`:

```json
{
  "mcpServers": {
    "gpusmarket": {
      "type": "stdio",
      "command": "gpusmarket",
      "args": ["mcp-serve"]
    }
  }
}
```

- **`--json` everywhere** — every command has machine-readable output.
- **Zero dependencies** — a single self-contained Node.js CLI. Nothing to audit but us.

## Honest billing

- **Per-second billing.** A 90-second experiment costs 90 seconds of GPU time.
- **A hold, not a charge.** Renting places a pre-auth hold (default $10) — it's released in full when you stop. You are never charged the hold.
- **No minimum charge.** Usage under $5 goes on your tab — no card charge at all — and is billed later as one combined charge (at $5 accrued, or 30 days at most). A 3¢ test costs you exactly 3¢. Usage of $5+ is charged exactly, immediately.
- **Receipts for everything**, with a full "where your money goes" breakdown.

## Commands

| Command | Description |
|---------|-------------|
| `init` | Quickstart guide (`--agent-schema` for the JSON command contract) |
| `signup` / `login` / `logout` / `whoami` | Account + API key management |
| `search` / `models` / `cheapest` | Browse the GPU marketplace |
| `rent` / `rentals` / `status` / `stop` | Rent, monitor, and stop GPUs |
| `chat` | Inference through your rental (streams, or pipe from stdin) |
| `pool create/list/add/remove` | Load-balance several rentals behind one key |
| `host setup` | List **your own** GPU for rent (auto-detects hardware) |
| `mcp-serve` | Start the MCP server (stdio) |

Run `gpusmarket --help` for the full reference, flags included.

## Earn with your GPU

Got a GPU sitting idle? List it in one command:

```bash
gpusmarket host setup          # auto-detects your GPU, creates the listing
npx gpusmarket-host --key KEY  # connect your machine — no port forwarding needed
```

You keep 90% of every rental, paid out to your Stripe account automatically.

## License

Proprietary — Copyright (c) 2026 Tyga.Cloud Ltd. All rights reserved. See LICENSE file.
