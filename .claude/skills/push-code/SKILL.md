---
name: push-code
description: "Push code with commit messages. Use when user wants to push changes, commit code. Handles branch creation from staging, file staging, professional commit messages (RB-XXXX format), and remote push with verification."
---

# Push Code Skill

## Purpose
Guide developers through the git workflow to safely push code to git with professional commit messages.

---

## When to Use
- User says "push my code", "commit and push", or "ready to push"
- User needs git workflow guidance
- User has changes and needs to push them
- User asks "how do I commit?"

---

## Information to Collect
1. **Ticket Number** — `RB-XXXX` (required)
2. **Files to stage** — run `git status` to show changes
3. **Commit message** — generate format: `RB-XXXX | Short description`

---

## Push Workflow (10 Steps)

### 1. Fetch Latest
```bash
git fetch origin
```


### 2. Check Current Branch
```bash
git branch
```

### 3. Create Feature Branch from Staging
```bash
git checkout -b RB-{Ticket-Number} origin/main
```
**Must branch from `origin/main`, not current HEAD.**

### 4. Verify Branch
```bash
git branch
git status
```
Expected: On branch `RB-XXXX`, tracking `origin/main`.

### 5. Show Changed Files
```bash
git status
```
Ask user: "Which files to stage?" (typically all with `git add .`)

### 6. Stage Files
```bash
git add .
```
Or specific files:
```bash
git add file1.php file2.phtml
```

Verify:
```bash
git status
```

### 7. Write Commit Message
Format: `RB-{Ticket-Number} | {Imperative description}`

**Examples:**
```
✅ RB-1234 | Add trader pricing display for B2B customers
✅ RB-5678 | Fix cart total calculation for bundled products
✅ RB-9012 | Refactor image processing to use cache
❌ RB-1234 | Work on trader pricing (vague)
```

### 8. Create Commit
```bash
git commit -m "RB-1234 | Add trader pricing display"
```

Verify:
```bash
git log --oneline -1
```

### 9. Push to Remote
```bash
git push origin RB-{Ticket-Number}
```

Expected: Branch pushed to Bitbucket.

### 10. Verify Push
```bash
git log --oneline -1
git branch -vv
```

---

## Quick Command Sequence

```bash
git fetch origin
git branch
git checkout -b RB-1234 origin/main
git status
git add .
git status
git commit -m "RB-1234 | Add trader pricing display"
git push origin RB-1234
git log --oneline -1
```

---

## Commit Message Rules

| Rule | Example |
|------|---------|
| Start with ticket | `RB-1234 \|` |
| Use pipe separator | `RB-1234 \| ` |
| Imperative mood | "Add", "Fix", "Update", "Refactor" |
| Specific description | "Fix cart rounding" not "Fixed bug" |
| Under 72 chars | Keep first line short |

---



