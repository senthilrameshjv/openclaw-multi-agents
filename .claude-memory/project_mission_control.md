---
name: Mission Control App
description: React + Express mission control dashboard for managing OpenClaw, hosted on the user's Mac
type: project
---

**Location:** `/Users/senthilrameshjv/Projects/OpenClaw/`

**Architecture:**
- `client/` — React + Vite + TypeScript + Tailwind (port 5173)
- `server/` — Express proxy (port 3001, bound to 127.0.0.1 only)

**Start commands:**
```bash
cd ~/Projects/OpenClaw/server && npm start       # proxy server
cd ~/Projects/OpenClaw/client && npm run dev     # React app
```

**Token:** stored in `server/.env` as `OPENCLAW_TOKEN` — never in browser

**Two backend channels:**
1. `/ssh/*` — SSH into server, run openclaw CLI commands, SFTP file read/write
2. `/proxy/*` — forwards to Tailscale HTTPS with Bearer token injected (mostly unused — OpenClaw API returns SPA HTML for most paths)

**Features implemented:**
- Overview: server status, gateway status, agent count
- Agents: per-agent tabs — Overview, Soul.md editor, Identity.md editor, Settings (model + bot token)
- Pairings: approve Telegram pairings by code
- Logs: live poll of `commands.log` + `config-audit.jsonl`, filterable by source
- Telegram: shows accounts + masked tokens
- Gateway: status + restart with confirmation

**Key bugs fixed:**
- File save not persisting: was using `echo | base64 -d` (shell length limit) → fixed with SFTP `putFile`
- After save showing stale data: fixed with `queryClient.setQueryData` on success
- Logs returning HTML: was calling `/proxy/logs` → fixed to use `/ssh/logs`
- Agent count showing 46: was counting all lines → fixed to count `^- \S+` matches
- Model validation allowing path traversal: added `..` check to regex

**How to apply:** If server crashes, restart with `npm start` in `server/`. Both processes must be running for the UI to work.
