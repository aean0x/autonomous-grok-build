# Grok Build Template

Baseline `config.toml` and org agent profiles for new Grok Build installations.

## Setup

1. Copy `config.toml` to `~/.grok/config.toml`, then review the `[mcp_servers]` section and remove or adjust entries to match the services this user actually has access to.
2. Copy the files from `agents/` to `~/.grok/agents/`.

The default agent is `adaptive`.

## Profiles

- `agents/adaptive.md` — Primary profile. Light by default, with on-demand escalation when complexity, risk, or ambiguity appears.
- `agents/high.md` — Maximum-rigor profile for high-stakes work where the cost of being wrong dominates the cost of being slow.

Both profiles supplement (and take precedence over) the internal defaults shipped at `~/.grok/agents/`. Read the individual `.md` files for the active instructions.

## TL;DR

- Default = light/fast — "do exactly what was asked; nothing more."
- Classify every task on four axes the moment you see it: **Ambiguity**, **Scope**, **Risk**, **Intent signals** → Low / Medium / High.
- Any Medium on any axis → escalate one rung. Any High → escalate two or more. Mid-task triggers also force a ramp (task grew, touches auth/security/concurrency, user says "thorough" or "right the first time").
- Tool ladder, lowest first: `todo_write` → `ask_user_question` → `enter_plan_mode` → `/implement --effort N` → `/best-of-n` → `/design` → `/execute-plan` → `/check` (required after any heavy work).
- Once a heavy phase is complete, drop back to light defaults for the next subtask. Do not stay heavy out of inertia.
- Always: discover MCP tools via `search_tool` immediately after the startup announcement; spawn subagents with the narrowest `capability_mode` plus worktree isolation; read handoff files in full.

The full 4-axis matrix, throttle rules, and recommended stacks live in `agents/adaptive.md`.

## Design notes

The profiles are deliberately self-contained *governance* — classification, throttle logic, and recommended stacks. They point at (never duplicate) the heavy SKILL orchestrators. Each profile ends with a **Canonical Internal References** section giving precise paths to the current `spawn_subagent` contract, effort-scaling details, persona injection rules, plan-mode gates, and MCP discovery behavior. When the bundled SKILLs or subagent docs change upstream, re-diff those pointers and bump the profile version note — keep the overlays lean.

Early and aggressive use of `search_tool` after the MCP connection announcement is emphasized because real environments often expose large but partial tool catalogs (fusion360, github, sequential-thinking, and a long tail of conditionally-available enterprise connectors).
