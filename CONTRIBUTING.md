# 🤝 Contributing to Repo Health Checker

Thank you for your interest in contributing! This guide will help you get started.

---

## 🚀 How to Contribute

### 1. Fork the Repository

Click the **Fork** button on the top right of this repo.

### 2. Clone Your Fork

```bash
git clone https://github.com/your-username/repo-health-checker.git
cd repo-health-checker
```

### 3. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 4. Make Your Changes

- Add new validation checks in `scripts/check.sh`
- Update documentation in `docs/`
- Improve the README

### 5. Test Locally

```bash
chmod +x scripts/check.sh
./scripts/check.sh
```

### 6. Commit with a Meaningful Message

```bash
git add .
git commit -m "feat: add your meaningful description of the change here"
```

> ⚠️ Commit messages must have **more than 5 words** — the CI will reject short messages!

### 7. Push and Open a Pull Request

```bash
git push origin feature/your-feature-name
```

Then open a **Pull Request** on GitHub targeting the `main` branch.

---

## ✅ PR Checklist

Before submitting your PR, make sure:

- [ ] `README.md` exists and has more than 5 lines
- [ ] `.gitignore` is present
- [ ] No `.env` or secret files are included
- [ ] Commit message is descriptive (more than 5 words)
- [ ] You've tested locally with `./scripts/check.sh`

---

## 💡 Ideas for Contributions

- Add a check for `LICENSE` file existence
- Add a check for trailing whitespace
- Add a check for TODO comments
- Improve error messages in the script
- Add more documentation

---

Thank you for helping make this project better! 🎉
