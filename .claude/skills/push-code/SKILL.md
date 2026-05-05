---
name: push-code
description: "Push code with commit messages. Use when the user wants to commit and push code. Handles branch creation from main, file staging, professional commit messages (RB-XXXX format), and remote push with verification."
---

# Push Code Skill

## Purpose
Guide developers through the git workflow to safely push code to git with professional commit messages.

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

### 3. Create Feature Branch from main
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
Ask user: "Which files to stage?" Prefer naming files explicitly.

### 6. Stage Files
Prefer named files:
```bash
git add file1.php file2.phtml
```

Use blanket staging only when the working tree is clean of generated/sensitive files:
```bash
git add .
```
**Caution:** avoid `git add .` if `.env`, `vendor/`, or generated/ directories show up in `git status` — they may be committed by accident.

Verify:
```bash
git status
```

### 7. Write Commit Message
Format: `RB-{Ticket-Number} | {Imperative description}`

**Good examples:**
```
RB-1234 | Add trader pricing display for B2B customers
RB-5678 | Fix cart total calculation for bundled products
RB-9012 | Refactor image processing to use cache
```

**Do NOT (too vague):**
```
RB-1234 | Work on trader pricing
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
Expected `git branch -vv` line for the current branch:
```
* RB-1234 abc1234 [origin/RB-1234] RB-1234 | Add trader pricing display
```
The `[origin/RB-1234]` marker confirms the branch is tracking the remote. If it shows `[origin/RB-1234: ahead 1]`, the push did not complete — re-run Step 9.

---

## Quick Command Sequence

```bash
git fetch origin
git branch
git checkout -b RB-1234 origin/main
git status
git add file1.php file2.phtml   # or `git add .` if working tree is clean
git status
git commit -m "RB-1234 | Add trader pricing display"
git push origin RB-1234
git branch -vv
```