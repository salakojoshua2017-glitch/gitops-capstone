# Getting Started

> **Goal:** Get a new contributor productive in under 1 hour.

---

## Step 1 — Environment Setup (15 min)

### Requirements
- Python 3.11 or higher
- Git
- A GitHub account
- A text editor (VS Code recommended)

### Install Python

**WSL/Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3.11 python3-pip -y
```

**macOS (Homebrew):**
```bash
brew install python@3.11
```

**Windows:**
Download from https://python.org and check "Add to PATH".

### Clone and Install
```bash
git clone https://github.com/salakojoshua2017-glitch/gitops-capstone.git
cd gitops-capstone
pip install -r requirements.txt
```

---

## Step 2 — Run the Tests (5 min)

Verify everything works before touching any code:
```bash
pytest test_app.py -v
```

Expected output:
```
test_app.py::test_health                PASSED
test_app.py::test_sum                   PASSED
test_app.py::test_reverse               PASSED
test_app.py::test_sum_with_negative     PASSED
test_app.py::test_sum_with_zero         PASSED
test_app.py::test_reverse_empty_string  PASSED
test_app.py::test_reverse_single_char   PASSED
test_app.py::test_reverse_palindrome    PASSED

8 passed
```

Also confirm linter is clean:
```bash
flake8 app.py test_app.py
```

No output means no issues.

---

## Step 3 — Branch Workflow (10 min)

Never commit directly to main. Always work on a feature branch.

### Create your branch
```bash
git checkout main
git pull origin main
git checkout -b feature/TRELLO-###-your-description
```

### Make changes and commit
```bash
git add .
git commit -m "[TRELLO-###] Brief description of what you did"
```

### Push your branch
```bash
git push origin feature/TRELLO-###-your-description
```

---

## Step 4 — Open a Pull Request (5 min)

1. Go to the repository on GitHub
2. Click "Compare & pull request" on your pushed branch
3. Title format: [TRELLO-###] Your description
4. Add a short description of what changed and why
5. Submit — CI will run automatically
6. Wait for the green check before requesting a review

---

## Step 5 — Troubleshooting

| Problem | Solution |
|---|---|
| ModuleNotFoundError: flask | Run pip install -r requirements.txt |
| flake8 reports errors | Fix the flagged lines and recommit |
| Tests fail locally | Check you have not modified app.py unexpectedly |
| CI fails but tests pass locally | Check Python version matches 3.11 |
| Push rejected | Run git pull origin main --rebase then push again |
| Merge button greyed out | CI must be green before merging is allowed |

---

## Quick Reference
```bash
python app.py                          # Run the app
pytest test_app.py -v                  # Run all tests
flake8 app.py test_app.py              # Run linter
git checkout -b feature/TRELLO-###-x  # Create feature branch
git commit -m "[TRELLO-###] Message"  # Commit with convention
git push origin feature/TRELLO-###-x  # Push branch
```
