# gpusmarket

**Rent real GPUs from the terminal. Built for AI agents.**

[![npm version](https://img.shields.io/npm/v/gpusmarket?color=cb3837&logo=npm)](https://www.npmjs.com/package/gpusmarket)
[![MCP — 32 tools](https://img.shields.io/badge/MCP-32%20tools-6E56CF?logo=modelcontextprotocol&logoColor=white)](#mcp-server)
[![Agent-native](https://img.shields.io/badge/agent-native-f97316)](#built-for-agents)
[![smithery badge](https://smithery.ai/badge/jyswee/gpusmarket)](https://smithery.ai/servers/jyswee/gpusmarket)

One command to sign up, one to rent, one to run inference. Per-second billing, no subscriptions, $0.50 minimum per rental. The CLI your coding agent can drive end-to-end: [GPUsMarket](https://gpusmarket.com).

> **`npm install` for GPUs. One command in, one command out.**

Renting a GPU usually means a signup form, a quota request, a support ticket, and a $50 minimum — before you've run a single token. GPUsMarket collapses that to three commands: everything from consumer RTX 4090s to datacenter H100s and MI300Xs, rentable by the second. And it's built so your **agent can sign up and rent by itself** — no human, no browser, no dashboard.

**Works with:** Claude Code · Cursor · Cline · Windsurf · Aider · Codex · any MCP client

<!-- HERO: money loop — install → signup → search → rent → chat (real inference) → stop → per-second bill -->
[![gpusmarket demo](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/hero-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/hero-stitched.mp4)

*Install to real inference in under a minute — [watch the full-res demo](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/hero-stitched.mp4).*

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

**Built so an agent can go from zero to running inference with no human in the loop** — sign up, rent, infer, and stop, all from the terminal or over MCP. This CLI is designed to be driven by AI coding agents (Claude Code, Cursor, Cline, Windsurf, Codex, Copilot), not just humans.

- **`gpusmarket init`** — in-terminal quickstart: detects your agent's config file, prints a ready-to-paste skill block, MCP setup, and next steps.
- **`gpusmarket init --agent-schema`** — the full command contract as JSON: every command, every flag, plus the rules agents must follow. Load it into context and your agent never hallucinates a flag.
- **`--json` everywhere** — every command has machine-readable output.
- **Zero dependencies** — a single self-contained Node.js CLI. Nothing to audit but us.

**Watch an agent drive it end-to-end** (click for the full-res video):

[![agent drives gpusmarket via MCP](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/claude-code-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/claude-code-stitched.mp4)

*Claude Code searches, rents, runs inference, and stops the GPU — no human in the loop.*

## MCP server

`gpusmarket mcp-serve` exposes **32 tools** over stdio — search, rent, status, stop, chat, host, pools, the whole surface. Add it to Claude Code:

```bash
claude mcp add gpusmarket -- gpusmarket mcp-serve
```

…or drop it into any MCP client's `.mcp.json`. The MCP server runs outside your project directory, so pass your API key via the `GPUSMARKET_API_KEY` environment variable:

```json
{
  "mcpServers": {
    "gpusmarket": {
      "type": "stdio",
      "command": "gpusmarket",
      "args": ["mcp-serve"],
      "env": { "GPUSMARKET_API_KEY": "gpu_your_key_here" }
    }
  }
}
```

No key yet? Run `gpusmarket signup` to provision one, or grab it from your [dashboard](https://gpusmarket.com).

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

Your GPU earns nothing while it sits idle. List it in one command — the CLI auto-detects your hardware, prints your host key, and the listing goes live in minutes. You keep **90%** of every rental, paid out to your Stripe account automatically. No port forwarding, no static IP, no open inbound ports.

**Three ways to host** (click any demo for the full-res video):

| Mac (Apple Silicon) | NVIDIA GPU | Docker sidecar |
|---|---|---|
| [![host on mac](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-mac-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-mac-stitched.mp4) | [![host on nvidia gpu](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-gpu-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-gpu-stitched.mp4) | [![host via docker](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-docker-stitched.gif)](https://prodmedia.tyga.host/public/tyga.cloud/landing/gpusmarket.com/cli/host-docker-stitched.mp4) |
| `gpusmarket host setup` | auto-detects CUDA + VRAM | `docker compose up -d` |

```bash
gpusmarket host setup          # auto-detects your GPU, creates the listing
npx gpusmarket-host --key KEY  # connect your machine — no port forwarding needed
```

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

## Features

- **Search** — filter the marketplace by GPU, price, or the exact model you need to run.
- **Rent** — one command returns an OpenAI/Ollama-compatible endpoint + key, ready for inference.
- **Chat** — stream inference straight through your rental, or pipe from stdin.
- **Pools** — put several rentals behind one endpoint and load-balance across them.
- **Host** — list your own GPU (Mac, NVIDIA, or Docker) and keep 90% of every rental.
- **Per-second billing** — receipts for everything, $0.50 minimum per rental, no subscriptions.
- **MCP server** — 32 tools over stdio for Claude Code, Cursor, Cline, Windsurf, any MCP client.
- **Agent-native** — `--json` everywhere plus `init --agent-schema` so agents never guess a flag.

## Why this exists

Renting a GPU should be as fast as `npm install`. Not a signup form, a quota request, a support ticket, and a $50 minimum. GPUsMarket is a marketplace where anyone can list an idle GPU and anyone — or any agent — can rent it by the second. This CLI is the agent-native front door to that marketplace. It's early and moving fast: if something's rough or missing, [open an issue](https://github.com/jyswee/gpusmarket/issues) — we read every one.

## Documentation

Full docs at [gpusmarket.com](https://gpusmarket.com). Run `gpusmarket init` for the interactive quickstart.

## License

Proprietary — Copyright (c) 2026 Tyga.Cloud Ltd. All rights reserved. See LICENSE file.
