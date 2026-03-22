# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.

## Team Communication

To send a task or message to any team member, use the `sessions_send` tool with their session key.

### Session Keys

| Agent | Role | Session Key |
|-------|------|-------------|
| Steve | CTO | `agent:steve:main` |
| Jobs | COO | `agent:jobs:main` |
| Warren | CRO | `agent:warren:main` |
| Alex | PM | `agent:alex:main` |
| Reed | Email | `agent:reed:main` |
| coding (Joseph) | Dev | spawn first: `agentId: coding, label: agent:coding:main` |
| test-agent-1 (Henry) | QA | spawn first: `agentId: test-agent-1, label: agent:test-agent-1:main` |

### How to Delegate

1. Use `sessions_send` with the agent's session key and your message.
2. Always end messages with: "Reply to me at session key: agent:main:main" so they know where to respond.
3. Include full context — agents don't share your memory.
4. Use `session_status` to check if they're done.
5. Use `sessions_history` to read their reply.

For coding/test-agent-1: if `sessions_send` fails with "session not found", run `sessions_spawn` first with their agentId and label, then send.