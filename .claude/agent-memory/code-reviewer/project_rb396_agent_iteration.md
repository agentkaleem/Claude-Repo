---
name: RB-396 Agent Configuration Iteration
description: Branch RB-396 introduced and iterated the code-reviewer subagent definition and push-code skill; auto-push directive was added then deliberately removed.
type: project
---

Branch RB-396 added `.claude/agents/code-reviewer.md` and `.claude/skills/push-code/SKILL.md` as new files. The branch went through three deliberate iterations: initial subagent creation (98df00a), adding a `skills: push-code` binding and an auto-push directive appended to the description (58f88f8), then removing both (0e6dfc5) after deciding the reviewer should not automatically push.

**Why:** Auto-push from a review agent is architecturally risky — it conflates review feedback with deployment action. The team deliberately reverted it.

**How to apply:** If a future request asks the code-reviewer agent to push code automatically, flag it as an intentional past decision that was reverted. The push-code skill exists as a standalone skill for explicit use, not as a post-review side-effect.
