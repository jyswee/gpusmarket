# gpusmarket

Rent GPUs from the terminal. Agent-first CLI for [GPUsMarket](https://gpusmarket.com).

## Quick Start

```bash
# Sign up (agent creates account for human)
npx gpusmarket signup --email you@example.com --tenant my-agent

# Search for GPUs
npx gpusmarket search --gpu RTX4090 --json

# Rent the cheapest available
npx gpusmarket rent --gpu RTX4090 --json

# Chat directly through your rented GPU
npx gpusmarket chat "What is 2+2?" --model qwen3:32b

# Stop when done
npx gpusmarket stop r_abc123
```

## Commands

| Command | Description |
|---------|-------------|
| `signup` | Create account + get API key |
| `login` | Save API key |
| `search` | Search available GPUs |
| `models` | List GPU models |
| `cheapest` | Find cheapest by VRAM |
| `rent` | Rent a GPU |
| `rentals` | List active rentals |
| `status` | Check rental status |
| `stop` | Stop a rental |
| `chat` | Send inference request |
| `pool create` | Create a GPU pool |
| `pool list` | List pools |

All commands support `--json` for agent-friendly output.

## License

Proprietary - Copyright (c) 2026 Tyga.Cloud Ltd. All rights reserved. See LICENSE file.
