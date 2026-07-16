# autonomous-grok-build

**Grok Build already has the tools. This repo teaches it when to use them.**

Grok Build ships plan mode, subagents, effort-scaled `/implement`, `/best-of-n`, `/design`, `/execute-plan`, `/check`, goal mode, MCP discovery, worktree isolation, and more. Out of the box most of that sits idle: the model just starts coding because nothing forces a deliberate choice about *which* machinery fits the work.

This repo is a thin overlay: a baseline `config.toml` and an **adaptive** agent profile with a skill decision matrix. Light by default. Escalates when ambiguity, scope, risk, or intent demand it. Drops back to light when the heavy phase is done. It does not reimplement skills; it only decides when to climb the ladder.

```
Ambiguity | Scope | Risk | Intent  →  Low / Medium / High
  Medium → +1 rung · High → +2+ rungs

light → plan → /implement --effort N → /best-of-n → /design → /execute-plan → /check
```

Details live in [`agents/adaptive.md`](agents/adaptive.md).

## Setup

```bash
cp config.toml ~/.grok/config.toml
mkdir -p ~/.grok/agents && cp agents/adaptive.md ~/.grok/agents/
```

Review `config.toml` for model names and any MCP servers you actually have. Default agent is `adaptive`.

## License

[GPL-3.0](LICENSE)
