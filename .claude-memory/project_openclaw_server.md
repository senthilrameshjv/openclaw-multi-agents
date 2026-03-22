---
name: OpenClaw Server Setup
description: Details of the remote OpenClaw server — SSH access, gateway config, Tailscale URL, auth token
type: project
---

OpenClaw runs on a remote Ubuntu ARM64 server at `178.104.66.69`.

**SSH access:** `ssh root@178.104.66.69` using `~/.ssh/id_ed25519`

**Gateway:** runs as systemd service `openclaw-gateway.service` on port 18789 (loopback only)

**Tailscale HTTPS URL:** `https://openclaw-ubuntu-arm64.tailb7a8d2.ts.net`

**Auth token:** stored in `/Users/senthilrameshjv/Projects/OpenClaw/server/.env` as `OPENCLAW_TOKEN` — never hardcode

**Config file:** `/root/.openclaw/openclaw.json`

**Restart gateway:** `openclaw gateway restart`

**Why:** Server was set up from scratch during this session — SSH key auth established, bun installed, QMD built from source.

**How to apply:** Always SSH via key. Never modify openclaw.json directly from the Mac — use the mission control or python3 scripts on the server.
