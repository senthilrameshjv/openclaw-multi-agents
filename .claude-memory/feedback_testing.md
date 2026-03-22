---
name: Testing and quality expectations
description: User expects everything to be tested and verified before handoff — no half-baked output
type: feedback
---

Test all features before declaring something done. The user explicitly said "I'm not happy with half baked product. make sure you test all different paths in each element."

**Why:** User was burned by untested features (logs broken, file save not persisting, agent count wrong).

**How to apply:** Before saying something is ready, run curl tests against all endpoints covering happy path, error paths, and security edge cases. Verify round-trips (write then read back). Check TypeScript compiles clean.
