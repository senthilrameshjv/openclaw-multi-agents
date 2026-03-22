# Migration: root → openclaw user

**Date:** 2026-03-22
**Status:** Complete

## What changed and why

Previously, the OpenClaw gateway and all 8 agents ran as `root` on the server. This meant any agent could read system files, write to `/etc`, install packages, or access any credential on the machine.

This was discovered when Joseph (coding agent) autonomously built an invoice processing pipeline — `api.js` running as a background server, reading email drafts, with full root access to the filesystem. Even though the data turned out to be synthetic, the same setup could have connected to real AWS credentials if any had been present.

The migration moves everything to an unprivileged `openclaw` user so agents are contained to their own workspace.

---

## What the openclaw user can and cannot do

| Capability | openclaw user |
|---|---|
| UID / GID | 1000 / 1000 (standard unprivileged) |
| Groups | `openclaw` only — no `sudo`, no `adm`, no `docker` |
| Run sudo | **No** — not in sudoers |
| Read `/root/` | **No** — permission denied |
| Write `/etc/` | **No** — permission denied |
| Write `/usr/` | **No** — permission denied |
| Outbound network | **Yes** — needed for Telegram, OpenRouter, AgentMail |
| Own home dir | **Yes** — full access to `/home/openclaw/` |
| Own `.openclaw/` | **Yes** — agents read/write their workspaces here |

Agents can still do their jobs (write files, run code, call APIs) but cannot touch the operating system, other users' files, or any path outside their home directory.

---

## File locations after migration

| What | Before | After |
|---|---|---|
| Config | `/root/.openclaw/openclaw.json` | `/home/openclaw/.openclaw/openclaw.json` |
| Agent workspaces | `/root/.openclaw/workspace-*` | `/home/openclaw/.openclaw/workspace-*` |
| Sessions / memory | `/root/.openclaw/agents/` | `/home/openclaw/.openclaw/agents/` |
| Scripts (cron) | `/root/.openclaw/scripts/` | `/home/openclaw/.openclaw/scripts/` |
| Logs | `/root/.openclaw/logs/` | `/home/openclaw/.openclaw/logs/` |
| bun runtime | `/root/.bun/` | `/home/openclaw/.bun/` |

The original `/root/.openclaw/` directory is **preserved untouched** as a rollback point.

---

## How openclaw-gateway is started

**Before:** Root user-level systemd service
`/root/.config/systemd/user/openclaw-gateway.service` (disabled, preserved)

**After:** System-level systemd service running as `openclaw`
`/etc/systemd/system/openclaw.service`

```ini
[Unit]
Description=OpenClaw Gateway
After=network.target

[Service]
Type=simple
User=openclaw
Environment=HOME=/home/openclaw
Environment=PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/openclaw/.bun/bin
WorkingDirectory=/home/openclaw
ExecStart=/usr/bin/openclaw gateway start
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Enabled on boot: `systemctl enable openclaw`

Useful commands:
```bash
systemctl status openclaw       # check status
systemctl restart openclaw      # restart gateway
journalctl -u openclaw -f       # tail logs
```

---

## Cron jobs

Migrated from root's crontab to openclaw user's crontab. Paths updated from `/root/` to `/home/openclaw/`.

```
TZ=UTC
0 13 * * 1-5   /usr/bin/node /home/openclaw/.openclaw/scripts/morning-meeting.js
*/5 * * * *    /usr/bin/node /home/openclaw/.openclaw/scripts/check-reed-inbox.js
```

---

## Mission Control changes

`server/.env` updated:
```
OPENCLAW_SSH_USER=openclaw
OPENCLAW_DATA_DIR=/home/openclaw/.openclaw
```

`server/index.js` updated: all hardcoded `/root/.openclaw` paths replaced with `${DATA_DIR}` (reads from `OPENCLAW_DATA_DIR` env var, falls back to `/root/.openclaw` for backwards compatibility).

---

## Rollback instructions

If anything breaks, SSH into the server as root and run:

```bash
bash /root/openclaw-rollback.sh
```

Then update `server/.env` on your Mac:
```
OPENCLAW_SSH_USER=root
# remove the OPENCLAW_DATA_DIR line
```

Restart the Mission Control server.

The rollback script:
1. Stops and disables the system openclaw service
2. Re-enables and starts the original root user-level service
3. Restores root's crontab with original paths

Everything needed for rollback is preserved:
- `/root/.openclaw/` — original data directory, untouched
- `/root/.config/systemd/user/openclaw-gateway.service` — original service file
- `/root/openclaw-rollback.sh` — the rollback script itself
