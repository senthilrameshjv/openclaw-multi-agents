---
name: QMD Memory Backend Setup
description: QMD is installed and configured as the memory backend for the main agent
type: project
---

QMD is set up as `memory.backend = "qmd"` in `/root/.openclaw/openclaw.json`.

**Binary:** `/root/.bun/bin/qmd` (built from source — `github.com/tobi/qmd`, no prebuilt dist included)

**Why built from source:** The npm/bun install doesn't include compiled dist — had to run `bun install && bun run build` inside the package directory.

**Index location:** `/root/.openclaw/agents/main/qmd/xdg-cache/qmd/index.sqlite`

**XDG env vars required to run qmd manually:**
```bash
export XDG_CONFIG_HOME=/root/.openclaw/agents/main/qmd/xdg-config
export XDG_CACHE_HOME=/root/.openclaw/agents/main/qmd/xdg-cache
```

**Collection:** `workspace` — indexes `/root/.openclaw/workspace/**/*.md` (9 files, 17 chunks)

**Embedding model:** `embeddinggemma-300M-Q8_0.gguf` (328MB, CPU only — no GPU on server)

**Test query:**
```bash
qmd vsearch "identity memory" --json --no-rerank
```

**How to apply:** If QMD stops working, check that bun is in PATH (`/root/.bun/bin`) and XDG vars are set. Re-run `qmd embed` if new files added to workspace.
