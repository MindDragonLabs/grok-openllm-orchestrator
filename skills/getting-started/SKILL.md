---
name: getting-started
description: First-run setup for the OpenLLM Orchestrator plugin. Use when the user installs this plugin, asks how OpenLLM works with Cursor or Grok Bot, or has not connected MCP yet.
---

# Getting started

Teach the user (and yourself) this split, then connect once.

| Role | Who | Does |
| --- | --- | --- |
| **Orchestrator** | Grok Bot or any Cursor agent | Plans, picks tools, asks for approvals, edits code, uses GitHub/Vercel/other connectors |
| **Model fabric** | OpenLLM gateway + `openllm mcp` | Routes inference across subscriptions/providers the user already pays for; exposes dashboard-like API tools, code/docs search, and memory |

This plugin does **not** replace GitHub, Vercel, or the editor. It wires OpenLLM so the orchestrator can manage account surfaces and run real coding tasks through the gateway.

Official product: [openllm.sh](https://openllm.sh). CLI source: [github.com/openllmsh/cli](https://github.com/openllmsh/cli). This plugin: [github.com/MindDragonLabs/grok-openllm-orchestrator](https://github.com/MindDragonLabs/grok-openllm-orchestrator).

## First-run script (one thing at a time)

Do not dump a questionnaire. After each answer, continue.

### 1. What this plugin does

In two or three sentences, explain dashboard mode vs development execution mode (see below). Ask whether they already have an OpenLLM account. If not, send them to [openllm.sh](https://openllm.sh) and wait.

### 2. CLI

Ask whether `openllm` is on their PATH.

If not, prefer the official installer (user should review the script before piping to a shell):

```sh
curl -fsSL "https://openllm.sh/api/setup/cli/install.sh" | bash
openllm version
```

**Dashboard one-click:** installing OpenLLM's own plugin from the gateway dashboard also installs the CLI, but that path is sandboxed and skips PATH/completion. They should run `~/.openllm/bin/openllm setup` once.

Do not invent other install URLs.

### 3. API key

Ask only for the key from the openllm.sh dashboard (`sk-llm` / API key). Tell them they will paste it into **Plugins → Configure** (`OPENLLM_API_KEY`), not into git.

If they paste a key in chat, use it to configure MCP env and **do not** echo it back, commit it, or write it into the repo.

### 4. Origin

Ask whether they use the default origin `https://openllm.sh`. Only if they say no, collect `OPENLLM_CLOUD_ORIGIN`.

### 5. Verify MCP

This plugin's `mcp.json` starts:

```text
openllm mcp
```

with `OPENLLM_API_KEY` and `OPENLLM_CLOUD_ORIGIN` substituted from plugin variables.

Ask them to reload MCP (Customize → MCP / Plugins). Then list **live** tools from the `openllm` server. Expect groups along these lines (names can shift; trust the live list):

- **Native gateway API** — one tool per OpenAPI operation from `/api/swagger` (models, chat/completions, usage/stats, keys, providers, config, …)
- **Code/docs search** — `openllm-context` / `claude-context`
- **Memory** — `openllm-memory` / `supermemory`

If tools are missing, switch to the **openllm-connect** skill (binary, key, origin).

### 6. Offer the next mode

Ask which they want first:

1. **Dashboard mode** — manage OpenLLM account surfaces via MCP (**openllm-dashboard**).
2. **Development execution mode** — a real coding task through the gateway + orchestrator tools (**openllm-dev-task**).

Grok Bot owners: also load **grok-bot-orchestrator**. Skills from this repo are not auto-packed into a shared bot template; they add OpenLLM as a custom connector and import or copy these skills.

## Two modes (remember this)

**Dashboard mode.** Use live MCP tools to inspect usage, models, keys/devices, providers, and config. Open [openllm.sh](https://openllm.sh) in a browser only when the API/MCP lacks that surface.

**Development execution mode.** Clarify the goal → pick a gateway model → use context/search → implement with normal coding tools → optionally hop to a specialist model through OpenLLM → report. You still own git and deploys.
