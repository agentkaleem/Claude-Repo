---
name: pr-description
description: "Write professional pull request descriptions following the RB-{Ticket Number} pattern. Use when creating a PR, writing a PR description, or when user asks to summarize changes for a pull request. Generates structured, clear descriptions with What, Why, How, Testing, Breaking Changes, and Deployment Notes sections. Suitable for Bitbucket, GitHub, or GitLab workflows."
---

# PR Description Skill

## Purpose

Every PR follows the `RB-{Ticket Number}` naming convention and uses a consistent structure that makes code review faster and the git history meaningful.

---

## When to Use This Skill

Use this skill whenever:

- A user says "write a PR description", "create a PR", or "summarize my changes"
- A user is preparing to push a branch and merge it into staging
- A user asks "what should I put in this PR?"
- A user has run `git diff` or `git log` output and wants it turned into a PR description
- A user mentions a ticket number like `RB-1234` in the context of code changes
- A user is creating a Bitbucket Pull Request and needs the description filled in

---

## Information to Collect Before Writing

Before generating a PR description, collect the following. Ask if not provided:

1. **Ticket Number** — `RB-XXXX` format (required for the title)
2. **Branch name** — e.g. `feature/trader-pricing`, `bugfix/cart-calculation`
3. **What changed** — ask user to describe in one sentence, or run:
   ```bash
   git diff staging...{branch-name} --stat
   git log staging..{branch-name} --oneline
   ```
4. **Why it was needed** — business reason, bug report, or feature request
5. **How to test** — manual steps or automated test commands
6. **Breaking changes** — schema changes, API changes, config changes

If the user provides a `git diff` or `git log` output, extract the information automatically without asking.

---

## PR Title Format

Every PR title must follow this exact pattern:

```
RB-{Ticket Number} | {Short imperative description}
```

**Rules:**
- Ticket number is mandatory — never omit it
- Use a pipe `|` separator between ticket and description
- Use imperative mood: "Add", "Fix", "Update", "Remove", "Refactor" — not "Added", "Fixing"
- Keep under 72 characters total
- Be specific — describe the actual change, not the ticket title

**Examples:**

```
✅ RB-1234 | Add trader pricing display for B2B customer group
✅ RB-5678 | Fix cart total calculation for bundled products
✅ RB-9012 | Refactor product image processing to use cache layer
✅ RB-3456 | Update Hyvä templates for mobile PLP responsiveness
✅ RB-7890 | Remove deprecated payment gateway integration

❌ RB-1234 | Trader pricing (too vague)
❌ RB-1234 | Fixed the bug (not imperative, too vague)
❌ RB-1234 | Added some stuff for traders and also updated templates and fixed a minor issue (too long)
```
---

## Full PR Description Template

Use this structure for every PR. Remove sections that are not applicable (e.g. no breaking changes → remove that section). Never leave sections empty — either fill them or remove them.

```markdown
## Summary

{2–3 sentences. What does this PR do and why does it matter?
Who benefits? What problem does it solve?}

---

##  What Changed

{Itemized list of actual changes, organized by layer or component.
Be specific about file names, class names, or module names where relevant.}

**Backend:**
- {Change 1}
- {Change 2}

**Frontend / Hyvä:**
- {Change 1}
- {Change 2}

**Configuration / Infrastructure:**
- {Change 1}

**Database / Schema:**
- {Change 1}

---

## Why

{Explain the business or technical reason this change was needed.
Link to the Jira/Bitbucket ticket. Explain what was broken or missing
and what the impact was.}

- **Ticket:** [RB-XXXX](link-to-ticket)
- **Root cause / Motivation:** {one sentence}
- **Impact if not fixed:** {one sentence — optional for features}

---
