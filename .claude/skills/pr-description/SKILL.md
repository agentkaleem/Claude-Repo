---
name: pr-description
description: "Write professional pull request descriptions following the RB-{Ticket Number} pattern. Use when creating a PR, writing a PR description, or when user asks to summarize changes for a pull request. Generates structured, clear descriptions with What, Why, How, Testing, Breaking Changes, and Deployment Notes sections. Suitable for Bitbucket, GitHub, or GitLab workflows."
compatibility: "Bitbucket, GitHub, GitLab — any Git-based platform with PR/MR functionality"
---

# PR Description Skill

## Purpose

Generate professional, structured pull request descriptions for the Royal Bathrooms development workflow. Every PR follows the `RB-{Ticket Number}` naming convention and uses a consistent structure that makes code review faster and the git history meaningful.

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

**PR Type Prefixes (optional, add after ticket number):**

| Type | When to Use | Example |
|------|-------------|---------|
| `[FEATURE]` | New functionality | `RB-1234 [FEATURE] | Add trader pricing` |
| `[FIX]` | Bug fix | `RB-5678 [FIX] | Fix cart total rounding` |
| `[REFACTOR]` | Code restructure, no behaviour change | `RB-9012 [REFACTOR] | Simplify image pipeline` |
| `[HOTFIX]` | Critical production fix | `RB-0001 [HOTFIX] | Disable broken payment provider` |
| `[CHORE]` | Dependency update, config change | `RB-3456 [CHORE] | Update Magento to 2.4.7` |

---

## Full PR Description Template

Use this structure for every PR. Remove sections that are not applicable (e.g. no breaking changes → remove that section). Never leave sections empty — either fill them or remove them.

```markdown
## 📋 Summary

{2–3 sentences. What does this PR do and why does it matter?
Who benefits? What problem does it solve?}

---

## ✅ What Changed

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

## 💡 Why

{Explain the business or technical reason this change was needed.
Link to the Jira/Bitbucket ticket. Explain what was broken or missing
and what the impact was.}

- **Ticket:** [RB-XXXX](link-to-ticket)
- **Root cause / Motivation:** {one sentence}
- **Impact if not fixed:** {one sentence — optional for features}

---

## 🔧 How

{Explain the approach taken. Focus on non-obvious decisions.
Explain why you chose this approach over alternatives.
Skip obvious implementation details.}

**Approach:**
{Paragraph or bullet points explaining the technical approach}

**Key decisions:**
- {Decision 1 and why}
- {Decision 2 and why}

**Alternatives considered:**
- {Alternative 1} — rejected because {reason}
- {Alternative 2} — rejected because {reason}

---

## 🧪 Testing

{Describe exactly how to verify this PR works correctly.
Steps must be reproducible by any reviewer.}

**Setup (if needed):**
```bash
bin/magento setup:upgrade
bin/magento indexer:reindex
bin/magento cache:flush
```

**Manual Testing Steps:**

1. {Step 1 — be specific, include URLs or navigation paths}
   - ✅ Expected: {what should happen}
2. {Step 2}
   - ✅ Expected: {what should happen}
3. {Edge case to verify}
   - ✅ Expected: {what should happen}

**Automated Tests:**
```bash
{command to run tests}
# Expected output: {describe passing state}
```

**Test Coverage:**
- {Test file or class added/modified}
- {What scenarios are covered}

---

## ⚠️ Breaking Changes

{List any changes that break backward compatibility.
If none, write "None." — do not remove this section.}

| Type | Description | Mitigation |
|------|-------------|------------|
| Schema | {e.g. Added column X to table Y} | {Run migration script} |
| API | {e.g. Response now includes trader_price field} | {Clients should handle null safely} |
| Config | {e.g. New env variable required} | {See .env.example} |
| Behaviour | {e.g. Trader group now sees different price} | {Communication sent to customer success} |

---

## 🚀 Deployment Notes

{Special instructions for deploying this PR.
Include order of operations, rollback plan, and monitoring steps.
Remove this section if standard deployment applies (just cache flush).}

**Order of operations:**
1. {Step 1}
2. {Step 2}
3. {Step 3}

**Rollback plan:**
{How to safely revert if issues are found in production}

**Feature flag:**
{If applicable — environment variable to enable/disable without redeploying}

**Post-deploy monitoring:**
- {What to watch in logs}
- {What metrics to check}

---

## 📸 Screenshots

{Add before/after screenshots for any UI changes.
Remove this section for backend-only changes.}

| Before | After |
|--------|-------|
| ![before]({url}) | ![after]({url}) |

---

## 🔗 Related

- **Ticket:** [RB-XXXX]
- **Depends on:** {RB-XXXX — must be merged first, or "None"}
- **Blocks:** {RB-XXXX — this must merge before that can proceed, or "None"}
- **Related PRs:** {links to related PRs, or "None"}

---

## ✔️ PR Checklist

- [ ] Branch created from `staging` (not `main`)
- [ ] Code follows project coding standards
- [ ] Self-review completed — read your own diff before requesting review
- [ ] Comments added for complex or non-obvious logic
- [ ] Tests added or updated
- [ ] No hardcoded credentials, API keys, or `.env` values in code
- [ ] `.env.example` updated if new environment variables were added
- [ ] `bin/magento setup:upgrade` tested locally
- [ ] Cache flushed and tested locally
- [ ] No new PHP warnings or errors in logs
- [ ] Hyvä templates validated in browser (if frontend changes)
- [ ] Mobile responsiveness checked (if UI changes)
- [ ] PR title follows `RB-XXXX | Description` format
```

---

## Minimal PR for Small Changes

For small bug fixes, typo corrections, or minor config updates, a shorter format is acceptable:

```markdown
## Summary
{One sentence describing the fix.}

## What Changed
- {File}: {what changed}

## Testing
1. {Step to verify fix}
   - ✅ Expected: {outcome}

## Breaking Changes
None.

**Ticket:** [RB-XXXX]({url})
```

---

## Real Examples

### Example 1: Feature PR

```markdown
## 📋 Summary

Adds a dedicated trader pricing tier for Royal Bathrooms B2B customers.
When a customer belonging to the "Trader" group logs in, product listing
pages (PLP) and product detail pages (PDP) now display their trader price
instead of the public retail price. This supports the B2B growth initiative
outlined in Q2 OKRs.

---

## ✅ What Changed

**Backend:**
- Added `trader_price` decimal product attribute (website-scoped) via data patch `AddTraderPriceAttribute`
- Added plugin `ApplyTraderPrice` on `Magento\Catalog\Model\Product::getFinalPrice()` to override price for Trader group
- Updated `di.xml` to register plugin for frontend area only

**Frontend / Hyvä:**
- Modified `product/price/final_price.phtml` to show "RRP £100 / Trade £75" for Trader group
- Added Alpine component `trader-price-badge` for session-aware price label
- No changes to base price rendering pipeline

**Configuration:**
- `etc/frontend/di.xml` — plugin registration
- `.env.example` — added `TRADER_GROUP_ID` variable

---

## 💡 Why

Traders were seeing retail pricing on the website, causing confusion and
manual price negotiations via phone. This feature gives Trader customers
their contracted pricing automatically on login.

- **Ticket:** [RB-1234](https://bitbucket.org/royalbathrooms/issues/1234)
- **Root cause / Motivation:** No customer-group-aware pricing on the frontend
- **Impact if not fixed:** Traders continue calling support for pricing, ~20 calls/week

---

## 🔧 How

**Approach:**
Used a Magento plugin on `getFinalPrice()` to intercept the price at runtime
and return `trader_price` when the logged-in customer belongs to the Trader group.
This approach avoids re-indexing and works transparently with Hyvä's price rendering.

**Key decisions:**
- Plugin over catalog price rules — trader prices are arbitrary (not formula-based), so a runtime plugin is cleaner
- Website-scoped attribute — Royal Bathrooms has UK/EU/US catalogs with different trader rates

**Alternatives considered:**
- Catalog price rules — rejected because they require a percentage formula; trader prices vary per product
- Tier prices per product — rejected because managing 50K products manually is not feasible

---

## 🧪 Testing

**Setup:**
```bash
bin/magento setup:upgrade
bin/magento indexer:reindex catalog_product_attribute
bin/magento cache:flush
```

**Manual Testing Steps:**

1. Log in as a Trader group customer
   - Navigate to any category page (PLP)
   - ✅ Expected: Product shows "RRP £100 / Trade £75" pricing
2. Add product to cart
   - ✅ Expected: Cart uses trader price (£75)
3. Log out
   - Return to same product page
   - ✅ Expected: Only retail price (£100) shown — no trader label

**Automated Tests:**
```bash
bin/magento test:unit Vendor_TraderPricing
# Expected: 3 tests, 3 passed, 0 failures
```

---

## ⚠️ Breaking Changes

| Type | Description | Mitigation |
|------|-------------|------------|
| Schema | New column `trader_price` in `catalog_product_entity_decimal` | Run `setup:upgrade` before deploying |
| Config | New env variable `TRADER_GROUP_ID` required | Set in `.env` — defaults to `4` if not set |

---

## 🚀 Deployment Notes

**Order of operations:**
1. Deploy code
2. Run `bin/magento setup:upgrade`
3. Run `bin/magento indexer:reindex`
4. Run `bin/magento cache:flush`
5. Verify on staging before production

**Rollback plan:**
Revert PR → run `setup:upgrade` → reindex → cache flush

**Post-deploy monitoring:**
- Watch `var/log/system.log` for `ApplyTraderPrice` exceptions
- Verify trader customer session prices on staging after deploy

---

## 🔗 Related

- **Ticket:** [RB-1234](https://bitbucket.org/royalbathrooms/issues/1234)
- **Depends on:** RB-1232 (attribute framework upgrade — merged ✅)
- **Blocks:** RB-1235 (trader account onboarding UI)
- **Related PRs:** None

---

## ✔️ PR Checklist

- [x] Branch created from `staging`
- [x] Self-review completed
- [x] Tests added
- [x] `.env.example` updated
- [x] `setup:upgrade` tested locally
- [x] Cache flushed and tested locally
- [x] PR title follows `RB-XXXX | Description` format
```

---

### Example 2: Bug Fix PR

```markdown
## 📋 Summary

Fixes incorrect cart total calculation when bundled products are added
with a discount coupon active. The subtotal was applying the discount
twice — once on the bundle parent and once on each bundle child item.

---

## ✅ What Changed

**Backend:**
- `Model/Quote/BundleDiscount.php` — fixed double-discount loop
- `Plugin/CartTotalPlugin.php` — added guard for bundle item type

---

## 💡 Why

Customers with discount codes were seeing incorrect (lower) totals on
bundled product carts. On checkout, the correct total was charged,
causing customer complaints and chargebacks.

- **Ticket:** [RB-5678](https://bitbucket.org/royalbathrooms/issues/5678)
- **Root cause:** Discount applied to bundle parent and re-applied to children
- **Impact if not fixed:** Customer complaints and support tickets (~5/day)

---

## 🔧 How

Added a type check in the discount loop to skip child items when the
parent bundle has already had the discount applied.

---

## 🧪 Testing

**Manual Testing Steps:**

1. Add a bundled product to cart
2. Apply discount code `TESTDISC10`
   - ✅ Expected: 10% off total, applied once
3. Verify cart total matches order confirmation total
   - ✅ Expected: Same amount at cart and checkout

---

## ⚠️ Breaking Changes
None.

---

## 🔗 Related
- **Ticket:** [RB-5678](https://bitbucket.org/royalbathrooms/issues/5678)
- **Depends on:** None
- **Blocks:** None
```

---

## Writing Style Guide

**Tone:** Professional, direct, and clear. Written for a technical audience.

| ✅ Good | ❌ Bad |
|--------|--------|
| "Fixes double-discount on bundle carts" | "Fixed stuff with bundles" |
| "Adds `trader_price` attribute via data patch" | "Did some attribute things" |
| "Reduces PLP queries from ~150 to 1 using index" | "Made it faster" |
| "Rejected catalog rules because prices aren't formula-based" | "This way was better" |

**Verb tense:** Use present tense in summaries ("Adds", "Fixes"), past tense in technical notes ("Tested with 50K products").

**Length:** Match length to complexity. A typo fix needs 5 lines. A new feature needs the full template.

---

## Using Claude Code to Auto-Generate PR Descriptions

Paste this prompt into Claude Code after making your changes:

```
Write a PR description for my current branch using the pr-description skill.

Ticket: RB-{XXXX}
Branch: {branch-name}
Summary: {one sentence about what you did}

Run `git diff staging...{branch-name} --stat` and `git log staging..{branch-name} --oneline` 
to get the file changes, then generate a full PR description using the RB-XXXX | Title format 
with all relevant sections: Summary, What Changed, Why, How, Testing, Breaking Changes, 
Deployment Notes, and PR Checklist.
```

Claude Code will:
- ✅ Analyze the git diff automatically
- ✅ Extract changed files and generate the "What Changed" section
- ✅ Draft testing steps based on what changed
- ✅ Flag potential breaking changes from schema or config files
- ✅ Format the title as `RB-XXXX | Description`

You then review, add business context, and paste into Bitbucket.

---

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Missing ticket number | Always start with `RB-XXXX \|` |
| Vague summary ("fixed bug") | Be specific: "Fix double-discount on bundle cart totals" |
| No testing steps | Add at least 2–3 reproducible manual steps with expected outcomes |
| Empty breaking changes section | Either fill it in or write "None." — never leave blank |
| Pasting huge code blocks | Reference file names and line numbers instead |
| No deployment notes for schema changes | Always add deployment order when `setup:upgrade` is needed |
| Missing `.env.example` update | If new env variables added, always update `.env.example` |

---
