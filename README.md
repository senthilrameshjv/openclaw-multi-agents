# openclaw-multi-agents

Agent workspace configuration for the Uncommon AI team running on OpenClaw.

## Server
- Host: `178.104.66.69` (Ubuntu ARM64)
- Gateway: systemd service `openclaw-gateway.service`, port 18789

## Agents

| Agent | Role | Model | Session Key |
|-------|------|-------|-------------|
| Marcel (main) | Chief of Staff / Orchestrator | google/gemini-3-flash-preview | `agent:main:main` |
| Steve | CTO | openrouter/qwen/qwen3-next-80b-a3b-instruct:free | `agent:steve:main` |
| Jobs | COO | google/gemini-3-flash-preview | `agent:jobs:main` |
| Warren | CRO | google/gemini-3-flash-preview | `agent:warren:main` |
| Alex | PM | google/gemini-3-flash-preview | `agent:alex:main` |
| Reed | Email | google/gemini-3-flash-preview | `agent:reed:main` |
| coding (Joseph) | Dev | openrouter/qwen/qwen3-coder:free | spawn: `agentId: coding, label: agent:coding:main` |
| test-agent-1 (Henry) | QA | openrouter/stepfun/step-3.5-flash:free | spawn: `agentId: test-agent-1, label: agent:test-agent-1:main` |

## Inter-Agent Communication

Marcel delegates to agents via `sessions_send` using session keys above.
All agents reply to Marcel at `agent:main:main`.
See `agents/main/TOOLS.md` for the full delegation guide.

## Directory Structure

```
agents/
  <agentId>/
    SOUL.md       — personality, role, responsibilities
    TOOLS.md      — local setup notes + session keys
    IDENTITY.md   — name and display settings
    USER.md       — who the agent is working for
    AGENTS.md     — workspace instructions
    HEARTBEAT.md  — proactive task checklist
.claude-memory/   — Claude Code session memory for this project
```

## Related
- Mission Control dashboard: https://github.com/senthilrameshjv/openclaw-mission-control
