---
name: OpenClaw Agents Configuration
description: The 3 agents on the server — their models, Telegram accounts, workspaces, and soul files
type: project
---

Three agents configured on the server:

| Agent | Model | Telegram Account | Workspace |
|---|---|---|---|
| `main` (default) | `nvidia/nemotron-3-super-120b-a12b:free` | `default` (bot: `8739994026:...`) | `/root/.openclaw/workspace` |
| `coding` | `openrouter/qwen/qwen3-coder:free` | `coding-account` (bot: `8768891581:...`) | `/root/.openclaw/workspace-coding` |
| `test-agent-1` | `stepfun/step-3.5-flash:free` | `test-agent-1` (bot: `8678091358:...`) | `/root/.openclaw/workspace-test-agent-1` |

**Routing:** `main` is default (no explicit binding). `coding` and `test-agent-1` have explicit telegram bindings in `openclaw.json`.

**Soul files:**
- `main` → default OpenClaw template (restored from https://github.com/openclaw/openclaw/blob/main/docs/reference/templates/SOUL.md)
- `coding` → custom "Senior Full-Stack Engineer / Self-Evolving Coder" soul (user-authored, v0.4)
- `test-agent-1` → custom "Adversarial Tester" soul (written this session)

**Identity:** main agent is named 🐚 DataRobot (set in IDENTITY.md)

**Why:** All models are free tier on OpenRouter. Models chosen based on role — nemotron-super for general, qwen3-coder for coding, step-3.5-flash for reasoning/QA.

**How to apply:** When changing models use mission control Agents → Settings tab, or `POST /ssh/agent/:id/model` on the proxy.
