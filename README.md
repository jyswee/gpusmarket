# gpusmarket

**Rent real GPUs from the terminal. Built for AI agents.**

[![npm version](https://img.shields.io/npm/v/gpusmarket?color=cb3837&logo=npm)](https://www.npmjs.com/package/gpusmarket)
[![MCP — 32 tools](https://img.shields.io/badge/MCP-32%20tools-6E56CF?logo=modelcontextprotocol&logoColor=white)](#mcp-server)
[![smithery badge](https://smithery.ai/badge/jyswee/gpusmarket)](https://smithery.ai/servers/jyswee/gpusmarket)

One command to sign up, one to rent, one to run inference. Per-second billing, no subscriptions, $0.50 minimum per rental. The CLI your coding agent can drive end-to-end: [GPUsMarket](https://gpusmarket.com).

**Works with:** Claude Code · Cursor · Cline · Windsurf · Aider · Codex · any MCP client

<!-- HERO: money loop — install → signup → search → rent → chat (real inference) → stop → per-second bill -->
[![gpusmarket demo](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/hero-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/hero-stitched.mp4)

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
gpusmarket chat "What is 2+2?" --model gemma3:4b

# Stop when done — you pay for exactly the seconds you used
gpusmarket stop RENTAL-ID
```

## Built for agents

This CLI is designed to be driven by AI coding agents (Claude Code, Cursor, Cline, Windsurf, Codex, Copilot), not just humans.

- **`gpusmarket init`** — in-terminal quickstart: detects your agent's config file, prints a ready-to-paste skill block, MCP setup, and next steps.
- **`gpusmarket init --agent-schema`** — the full command contract as JSON: every command, every flag, plus the rules agents must follow. Load it into context and your agent never hallucinates a flag.
- **`--json` everywhere** — every command has machine-readable output.
- **Zero dependencies** — a single self-contained Node.js CLI. Nothing to audit but us.

## MCP server

`gpusmarket mcp-serve` exposes **32 tools** over stdio — search, rent, status, stop, chat, host, pools, the whole surface. Add it to Claude Code:

```bash
claude mcp add gpusmarket -- gpusmarket mcp-serve
```

…or drop it into any MCP client's `.mcp.json`:

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

## Core capabilities

Each demo links to the full-resolution MP4.

| Browse the marketplace | Manage your rentals | Load-balance a pool |
|---|---|---|
| [![browse](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/browse-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/browse-stitched.mp4) | [![manage](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/manage-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/manage-stitched.mp4) | [![pools](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/pools-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/pools-stitched.mp4) |
| `search` · `cheapest` · `models` | `rentals` · `status` · `stop` | `pool create` · `add` · `list` |

```bash
# Browse
gpusmarket search --gpu "RTX 4090"      # filter by GPU, price, model
gpusmarket cheapest --model gemma3:4b   # the single cheapest node that serves a model
gpusmarket models                       # every model available across the marketplace

# Manage
gpusmarket rentals                      # your active rentals
gpusmarket status RENTAL-ID             # live status + running cost
gpusmarket stop RENTAL-ID               # stop, pay for the seconds you used

# Pool — one endpoint, several rentals behind it
gpusmarket pool create my-pool
gpusmarket pool add my-pool RENTAL-ID
gpusmarket pool list
```

## Honest billing

- **Per-second billing.** A 90-second experiment costs 90 seconds of GPU time.
- **A hold, not a charge.** Renting places a pre-auth hold (default $10) — it's released in full when you stop. You are never charged the hold.
- **$0.50 minimum per rental.** You pay per second for the compute you consume, subject to a $0.50 minimum charge per rental (disclosed when you rent). When you stop, your card is charged the exact usage cost, or the $0.50 minimum — whichever is greater.
- **Receipts for everything**, with a full "where your money goes" breakdown.

## Earn with your GPU

<!-- HOST: host setup auto-detects the GPU, prints the host key, listing goes live -->
[![host setup](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-mac-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-mac-stitched.mp4)

Got a GPU sitting idle? List it in one command:

```bash
gpusmarket host setup          # auto-detects your GPU, creates the listing
npx gpusmarket-host --key KEY  # connect your machine — no port forwarding needed
```

You keep 90% of every rental, paid out to your Stripe account automatically.

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

## Why this exists

Renting a GPU should be as fast as `npm install`. Not a signup form, a quota request, a support ticket, and a $50 minimum. GPUsMarket is a marketplace where anyone can list an idle GPU and anyone — or any agent — can rent it by the second. This CLI is the agent-native front door to that marketplace.

## Documentation

Full docs at [gpusmarket.com](https://gpusmarket.com). Run `gpusmarket init` for the interactive quickstart.

## License

Proprietary — Copyright (c) 2026 Tyga.Cloud Ltd. All rights reserved. See LICENSE file.
