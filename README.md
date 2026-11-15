# goose-emino-vps

Minimal goose setup: Kimi K3.1 Pro Max plans/reviews; fastest uncensored DeepSeek implements. No Hermes, Docker, local models or MCP servers.

## Install

1. Copy `config/goose/` contents into `~/.config/goose/`.
2. Copy `.env.example` to a protected env file and fill both keys. Never commit it.
3. Export both variables in goose's environment.
4. Run the checks in `tests/canary.md`.

Settings: max reasoning, 126,976 output-token ceiling, telemetry off. DeepSeek route: Lyber → Hopper → Abliteration.

## Roles

- Planner/reviewer: provider `402router`, model `k3.1-pro`.
- Worker: provider `allmodels_fast`, model `deepseek/deepseek-v4.1-flash-abliterated`.
