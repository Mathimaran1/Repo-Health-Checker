# 🏗️ Architecture — Repo Health Checker

This document explains the design decisions behind the Repo Health Checker project and how each piece fits together.

---

## 📁 Why Folders Are Separated

The project follows a **separation of concerns** principle — each folder has a single, clear responsibility:

```
.github/workflows/   →  CI/CD automation (what triggers the checks)
scripts/             →  Validation logic (what the checks actually do)
docs/                →  Documentation (why things are built this way)
```

### Benefits of This Separation

- **Clarity** — A new contributor can instantly find what they're looking for
- **Maintainability** — Changes to the workflow don't require touching the script, and vice versa
- **Scalability** — You can add new scripts, workflows, or docs without reorganizing
- **Convention** — This mirrors how real-world repositories are structured

> **Real-World Example:** In a production codebase, you might have dozens of workflows and scripts. Keeping them organized from the start prevents chaos later.

---

## 🧩 Why Scripts Are Modular

The validation script (`scripts/check.sh`) is built with **modular functions** — each check is its own self-contained function:

```
check_readme()       →  Validates README.md
check_gitignore()    →  Validates .gitignore
check_no_secrets()   →  Scans for .env files
```

### Why Not One Big Script?

A single long script with all logic mixed together would:
- Be hard to read and understand
- Be difficult to debug when something fails
- Make it painful to add new checks
- Be impossible to test individual checks in isolation

### How Modular Design Helps

| Benefit | Explanation |
|---------|-------------|
| **Readability** | Each function has a descriptive name that explains what it does |
| **Debugging** | When a check fails, you know exactly which function to look at |
| **Extensibility** | Adding a new check means writing a new function and calling it in `main()` |
| **Reusability** | Functions can be reused or adapted for other projects |

### Adding a New Check

To add a new validation, you simply:

1. Write a new function:
   ```bash
   check_license() {
     if [ ! -f "LICENSE" ]; then
       print_fail "LICENSE file not found"
       return 1
     fi
     print_pass "LICENSE exists"
     return 0
   }
   ```

2. Call it from `main()`:
   ```bash
   if ! check_license; then
     all_passed=false
   fi
   ```

That's it. No other code needs to change.

---

## 🔄 How PR-Based CI Works

### What Is CI?

**Continuous Integration (CI)** is the practice of automatically testing code changes before they are merged. Instead of relying on humans to catch every issue, automated systems validate the code.

### Why PR-Based (Not Push-Based)?

There are two common CI trigger strategies:

| Strategy | Trigger | When Checks Run |
|----------|---------|-----------------|
| **Push-based** | `on: push` | Every time code is pushed to any branch |
| **PR-based** | `on: pull_request` | Only when a PR is opened or updated |

This project uses **PR-based CI** because:

1. **Gatekeeping** — Checks run before code enters `main`, not after
2. **Efficiency** — Checks only run when code is ready for review, not on every experimental push
3. **Visibility** — Results appear directly on the PR page, making it easy to see what passed or failed
4. **Blocking** — Failed checks can prevent merging, protecting the main branch

### The Flow

```
Feature Branch                    Main Branch
     │                                │
     │  1. Developer pushes code      │
     │                                │
     │  2. Developer opens PR ──────► │
     │                                │
     │  3. GitHub Actions triggers    │
     │     └── check.sh runs         │
     │                                │
     │  4a. ✅ Checks pass            │
     │      └── PR can be merged ──► │ (code enters main)
     │                                │
     │  4b. ❌ Checks fail            │
     │      └── PR is blocked        │
     │      └── Developer fixes      │
     │      └── Push again → re-run  │
```

### What Happens on the PR Page

When GitHub Actions runs:

- A **yellow dot** appears while checks are running
- A **green checkmark** (✅) appears if all checks pass
- A **red X** (❌) appears if any check fails
- Clicking the status shows detailed logs from the script

---

## 🤖 Why Automation Improves Software Quality

### The Problem Without Automation

Without automated checks, teams rely entirely on manual code review:

- Reviewers might forget to check for `.env` files
- Someone might approve a PR without a proper README
- Different reviewers apply different standards
- Humans get tired; scripts don't

### How Automation Solves This

| Problem | Automated Solution |
|---------|-------------------|
| Forgotten checks | Scripts run every single time, no exceptions |
| Inconsistent standards | The same rules apply to every PR |
| Slow reviews | Checks run in seconds |
| Human error | Scripts don't get tired or distracted |
| Secret leaks | Automated scanning catches `.env` files instantly |

### The Key Insight

> **Automation doesn't replace human code review — it enhances it.**

Humans should focus on:
- Does the logic make sense?
- Is the code well-designed?
- Are there edge cases?

Machines should handle:
- Does the README exist?
- Are there secret files?
- Is the repo structure correct?

By letting automation handle the repetitive checks, human reviewers can focus on what actually requires human judgment.

---

## 🎯 Summary

| Design Decision | Reason |
|----------------|--------|
| Separated folders | Clear responsibility, easy navigation |
| Modular script functions | Easy to read, debug, and extend |
| PR-based CI trigger | Checks code before it enters main |
| Automated validation | Consistent, fast, and reliable quality checks |

This architecture is intentionally simple — but it reflects the same principles used in production systems at companies of all sizes.
