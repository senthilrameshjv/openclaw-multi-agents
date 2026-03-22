---
name: Do not accidentally modify server files during testing
description: Avoid overwriting live workspace files (soul.md etc) when running tests
type: feedback
---

During testing, accidentally overwrote `/root/.openclaw/workspace/SOUL.md` with the wrong content (test-agent soul) while trying to verify file writes. Had to restore from the official template.

**Why:** Used the same temp file for both testing and "restoring", which replaced the live file with wrong content.

**How to apply:** When testing file write endpoints, use a throwaway file or append a marker and immediately revert. Never use a production agent's soul/identity file as the test target. Always confirm what file is being written before executing.
