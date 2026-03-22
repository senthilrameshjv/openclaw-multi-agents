---
name: OpenClaw Agents Configuration
description: All 8 agents on the server — models, Telegram accounts, workspaces, session keys, inter-agent comms
type: project
---

8 agents configured on the server:

| Agent | Name | Model | Session Key | Workspace |
|---|---|---|---|---|
| `main` | Marcel | `google/gemini-3-flash-preview` | `agent:main:main` | `/root/.openclaw/workspace` |
| `coding` | Joseph | `openrouter/qwen/qwen3-coder:free` | `agent:coding:main` (spawn first) | `/root/.openclaw/workspace-coding` |
| `test-agent-1` | Henry | `openrouter/stepfun/step-3.5-flash:free` | `agent:test-agent-1:main` (spawn first) | `/root/.openclaw/workspace-test-agent-1` |
| `steve` | Steve | `openrouter/qwen/qwen3-next-80b-a3b-instruct:free` | `agent:steve:main` | `/root/.openclaw/workspace-steve` |
| `jobs` | Jobs | `google/gemini-3-flash-preview` | `agent:jobs:main` | `/root/.openclaw/workspace-jobs` |
| `warren` | Warren | `google/gemini-3-flash-preview` | `agent:warren:main` | `/root/.openclaw/workspace-warren` |
| `alex` | Alex | `google/gemini-3-flash-preview` | `agent:alex:main` | `/root/.openclaw/workspace-alex` |
| `reed` | Reed | `google/gemini-3-flash-preview` | `agent:reed:main` | `/root/.openclaw/workspace-reed` |

**Telegram accounts:**
- `default` → Marcel (bot: `8739994026:...`)
- `coding-account` → Joseph (bot: `8768891581:...`)
- `test-agent-1` → Henry (bot: `8678091358:...`)
- Steve, Jobs, Warren, Alex, Reed have no Telegram binding (internal only)

**Marcel's role:** Chief of Staff / Orchestrator. Delegates to all other agents via `sessions_send`.

**Inter-agent comms:**
- All agents reply to Marcel at `agent:main:main`
- Email to CEO goes via Reed at `agent:reed:main` using EMAIL REQUEST format
- Reed's inbox: `reed_uncommon@agentmail.to`
- agentmail skill copied to Reed's workspace: `/root/.openclaw/workspace-reed/skills/agentmail/`

**OpenRouter API key hit USD spend limit** — Marcel switched to `google/gemini-3-flash-preview` which works. Avoid adding Claude/paid OpenRouter models to fallback list.

**Repo:** https://github.com/senthilrameshjv/openclaw-multi-agents

**How to apply:** Session keys for coding/test-agent-1 need `sessions_spawn` first before `sessions_send`. All others connect directly.
