# Moved: use openllm-bots

This flat plugin repo is **superseded** by the standardized monorepo:

**→ [https://github.com/MindDragonLabs/openllm-bots](https://github.com/MindDragonLabs/openllm-bots)**

| What you want | Where it lives now |
| --- | --- |
| Grok Bot skills + setup | [`bots/grok`](https://github.com/MindDragonLabs/openllm-bots/tree/main/bots/grok) |
| Cursor plugin | [`bots/cursor`](https://github.com/MindDragonLabs/openllm-bots/tree/main/bots/cursor) |
| Muse / Hermes (stubs) | [`bots/muse`](https://github.com/MindDragonLabs/openllm-bots/tree/main/bots/muse), [`bots/hermes`](https://github.com/MindDragonLabs/openllm-bots/tree/main/bots/hermes) |
| Shared architecture + OpenLLM connect | [`shared/`](https://github.com/MindDragonLabs/openllm-bots/tree/main/shared) |

Same idea as before: **orchestrator = the bot**, **model fabric = OpenLLM** via `openllm mcp`. The monorepo just gives each bot its own folder.

Migration map: [MIGRATION.md](https://github.com/MindDragonLabs/openllm-bots/blob/main/MIGRATION.md).

This repository is kept as a pointer so old links still resolve. New work goes in **openllm-bots**.
