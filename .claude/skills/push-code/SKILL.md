---
name: push-code
description: "Push code to Bitbucket with professional commit messages. Use when user wants to push changes, commit code, or needs git workflow guidance. Handles branch creation from staging, file staging, professional commit messages (RB-XXXX format), and remote push with verification."
compatibility: "Bitbucket, GitHub, GitLab"
---

# Push Code Skill

## Purpose
Guide developers through the git workflow to safely push code to Bitbucket with professional commit messages following Royal Bathrooms standards.

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
git checkout -b RB-{Ticket-Number} origin/staging
```
**Must branch from `origin/staging`, not current HEAD.**

### 4. Verify Branch
```bash
git branch
git status
```
Expected: On branch `RB-XXXX`, tracking `origin/staging`.

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

### 7. Write Professional Commit Message

**Format:**
```
RB-{Ticket-Number} | {Short description}

{Detailed explanation (optional, for complex changes)}
```

**Single-line commit (most common):**
```bash
git commit -m "RB-1234 | Add trader pricing display for B2B customers"
```

**Multi-line commit (for complex changes):**
```bash
git commit -m "RB-1234 | Add trader pricing display for B2B customers" -m "

- Added trader_price decimal product attribute (website-scoped)
- Plugin on getFinalPrice() returns trader price for Trader group
- Updated Hyvä templates to show RRP + Trade price
- Tested on simple, configurable, and grouped products
"
```

**Or use editor:**
```bash
git commit
# Opens editor for multi-line message
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
git checkout -b RB-1234 origin/staging
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
| Under 72 chars (line 1) | Keep first line short |
| Explain WHY not HOW | "Fixes double-discount" not "Changed discount loop" |
| Include impact (if relevant) | "Reduces load time by 40%" or "Fixes customer billing" |

---

## Writing Professional Commit Messages

### Structure

**Line 1:** Ticket + short description (required)
```
RB-1234 | Add trader pricing display
```

**Line 2:** Blank line (separator)

**Lines 3+:** Detailed explanation (optional but recommended for complex changes)
```
- What was changed and why
- Technical approach or solution
- Impact or benefits
- Edge cases or limitations
```

### Best Practices

**DO:**
- ✅ Describe the change clearly: "Add trader_price attribute"
- ✅ Explain the problem being solved: "Traders were seeing retail prices, causing confusion"
- ✅ Mention impact: "Reduces support calls by ~70%"
- ✅ List multiple changes: Use bullet points
- ✅ Include testing info: "Tested on simple, configurable, grouped products"
- ✅ Reference related tickets: "Related to RB-1235 (onboarding UI)"

**DON'T:**
- ❌ Use vague language: "Fixed stuff", "Work on feature"
- ❌ Write in past tense: "Added" → use "Add"
- ❌ Paste huge code blocks: Reference files instead
- ❌ Use internal jargon without context
- ❌ Make personal comments: Keep it professional

### Real Examples

**Feature: Complete & Professional**
```
RB-1234 | Add trader pricing display for B2B customers

Adds a dedicated pricing tier for Trader group customers on PLP and PDP.
Traders now see their contract price (RRP £100 / Trade £75) automatically
when logged in.

Technical Approach:
- Added trader_price decimal product attribute (website-scoped)
- Plugin on getFinalPrice() returns trader price for Trader group
- Updated Hyvä templates to show RRP + Trade price
- Plugin skips non-Trader groups for zero performance impact

Impact:
- Eliminates manual phone negotiations for trader pricing
- Reduces support calls by ~70%
- Supports Q2 B2B growth OKR

Tested:
- Simple products: ✓
- Configurable products: ✓
- Grouped products: ✓
- Cart calculation: ✓
- Checkout total: ✓
```

**Bug Fix: Concise & Actionable**
```
RB-5678 | Fix cart total calculation for bundled products

Problem: Discount applied twice — once on bundle parent, once on children
Solution: Added type check in discount loop to skip children items
Impact: Eliminates customer billing discrepancies (~5 complaints/day)

Testing:
1. Add bundled product + discount code TESTDISC10
2. Verify cart total = order total at checkout
3. No double discount applied
```

**Refactor: Clear Rationale**
```
RB-9012 | Refactor image processing to use cache layer

Moved product image resizing from runtime to Redis cache.
Images pre-cached during product upload instead of on-demand.

Performance Impact:
- PLP load time: 156ms → 92ms (40% faster)
- Tested with 50K products
- Backwards compatible: No API changes

Approach:
- Cache layer added to Vendor\ImageProcessing\Cache
- Existing public API unchanged
- Async job clears cache on product update
```

**Chore: Brief & Professional**
```
RB-3456 | Update Hyvä to 1.2.5 and Magento to 2.4.7

- Hyvä: 1.2.4 → 1.2.5 (bug fixes, performance improvements)
- Magento: 2.4.6 → 2.4.7 (security patches, compatibility fixes)
- Tested on staging environment
- No breaking changes for existing extensions
- Composer lock file updated
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



