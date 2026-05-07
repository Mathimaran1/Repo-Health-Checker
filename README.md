# 🏥 Repo Health Checker

[![Repo Health Check](https://github.com/Mathimaran1/Repo-Health-Checker/actions/workflows/check.yml/badge.svg)](https://github.com/Mathimaran1/Repo-Health-Checker/actions/workflows/check.yml)
A beginner-friendly DevOps mini project that **automatically validates repository quality** whenever a Pull Request is created.

This project simulates how real companies review code before merging it into the main branch — using **GitHub Actions** and a **Bash validation script** to act as an automated quality inspector.

---

## 🎯 What Does This Project Do?

When a developer opens a Pull Request, GitHub Actions automatically runs a series of health checks on the repository. If all checks pass, the PR is safe to merge. If any check fails, the PR is blocked until the issues are fixed.

**Think of it like airport security for your code** — before anything enters the `main` branch, it goes through automated inspection.

---

## 🔄 How the CI/CD Workflow Works

```
Developer creates a feature branch
        │
        ▼
Developer pushes code
        │
        ▼
Developer opens a Pull Request
        │
        ▼
GitHub Actions automatically starts
        │
        ▼
Validation script runs checks
        │
        ├── ✅ All checks pass → PR is safe to merge
        │
        └── ❌ Any check fails → PR is blocked
```

### Step-by-Step

1. **Branch** — You create a new branch from `main` (e.g., `feature/add-docs`)
2. **Code** — You make your changes and push them
3. **PR** — You open a Pull Request targeting `main`
4. **CI Triggers** — GitHub Actions detects the PR and starts the workflow
5. **Checks Run** — The `scripts/check.sh` script validates the repo
6. **Result** — You see a green checkmark (pass) or red X (fail) on the PR

---

## ✅ Validation Rules

The health checker runs these automated checks:

| # | Check | What It Does | Why It Matters |
|---|-------|-------------|----------------|
| 1 | **README Exists** | Verifies `README.md` is present | Every project needs documentation |
| 2 | **README Length** | Ensures README has more than 5 lines | Documentation should be meaningful |
| 3 | **Gitignore Exists** | Verifies `.gitignore` is present | Prevents repo clutter and junk files |
| 4 | **No Secret Files** | Scans for `.env` files | Prevents accidental secret/credential leaks |
| 5 | **Commit Message** | Checks commit message has >5 words | Encourages meaningful commit messages |

---

## 📁 Folder Structure

```
repo-health-checker/
├── .github/
│   └── workflows/
│       └── check.yml        # GitHub Actions workflow definition
│
├── scripts/
│   └── check.sh             # Bash validation script with modular checks
│
├── docs/
│   └── architecture.md      # Project architecture & design decisions
│
├── README.md                # Project documentation (this file)
├── .gitignore               # Files to exclude from version control
└── LICENSE                  # MIT License
```

---

## 🚀 How to Use This Project

### Testing Locally

```bash
chmod +x scripts/check.sh
./scripts/check.sh
```

---

## 🛡️ Why Automated Checks Matter

- **Manual reviews miss things** — Automated checks catch issues humans overlook
- **Consistency** — Every PR goes through the same validation process
- **Speed** — Checks run in seconds, not hours
- **Prevention** — It's easier to block bad code than to fix it after merging

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
