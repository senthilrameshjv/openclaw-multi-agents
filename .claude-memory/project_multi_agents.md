---
name: openclaw-multi-agents Project
description: GitHub repo for all agent workspace configs + inter-agent communication setup
type: project
---

**Repo:** https://github.com/senthilrameshjv/openclaw-multi-agents

**What it is:** All agent workspace markdown files (SOUL.md, TOOLS.md, IDENTITY.md, USER.md, AGENTS.md, HEARTBEAT.md) for all 8 agents, version-controlled on GitHub for mobile editing via Claude Code.

**Structure:**
```
agents/<agentId>/   — workspace files for each agent
.claude-memory/     — Claude Code session memory (project continuity)
```

**What was built this session (2026-03-22):**

1. **Inter-agent session keys** — Marcel's TOOLS.md documents all 7 team session keys so he delegates automatically without being told to use sessions_send
2. **Bidirectional reply** — All agents' TOOLS.md tells them to reply to Marcel at `agent:main:main`. Marcel tells agents his session key in every outbound message.
3. **Inter-agent email via Reed** — All agents can send EMAIL REQUEST to Reed at `agent:reed:main`. Reed's SOUL.md handles receiving, polishing, sending, and confirming. Reed's inbox: `reed_uncommon@agentmail.to`
4. **Tested end-to-end:** Marcel → Steve (sessions_send ✅) → Marcel → Reed (EMAIL REQUEST ✅) → email delivered to senthilrameshjv@gmail.com ✅

**Branch merged:** `claude/project-assessment-REhjY` — inter-agent email delegation. Fix added before merge: Reed's TOOLS.md was missing inbox address and send script path.

**Planned but not built:** CI/CD with self-hosted GitHub Actions runner
- `test.yml` — spins up staging-main agent (no Telegram), patches session key `agent:main:main` → `agent:staging-main:main`, runs test, tears down
- `deploy.yml` — on merge to main, syncs all agent workspaces to server
- Decision deferred — user wants to think through the approach first

**How to apply:** When editing agent configs from mobile, changes go to a branch first, get reviewed, then merged to main. Currently manual sync to server — CI/CD not yet set up.
