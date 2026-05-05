---
name: RB-396 Agent Configuration Iteration
description: The code-reviewer subagent must not push code automatically; auto-push was deliberately removed after being trialed.
type: project
---

The code-reviewer subagent must not push code automatically. An earlier iteration on this project added a `skills: push-code` binding and an auto-push directive to the reviewer; both were deliberately removed.

**Why:** Auto-push from a review agent is architecturally risky — it conflates review feedback with deployment action. The team deliberately reverted it.

**How to apply:** If a future request asks the code-reviewer agent to push code automatically, flag it as an intentional past decision that was reverted. The push-code skill exists as a standalone skill for explicit use, not as a post-review side-effect.

**Provenance:** Decision finalized on branch RB-396 (May 2026). The revert and the surrounding iteration history can be traced via `git log --oneline` on RB-396 — look for the commit that removes the `skills: push-code` binding and the auto-push directive from `.claude/agents/code-reviewer.md`.
