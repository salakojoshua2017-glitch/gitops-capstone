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

**macOS (Homebrew):**
```bash
brew install python@3.11
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3.11 python3-pip -y
```

**Windows:**
Download from [python.org](https://www.python.org/downloads/) and check "Add to PATH".

### Clone & Install

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
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

8 passed in X.XXs
```

Also run the linter to confirm a clean baseline:

```bash
flake8 app.py test_app.py
```

No output = no issues.

---

## Step 3 — Branch Workflow (10 min)

**Never commit directly to `main`.** Always work on a feature branch.

### Create your branch

Find your Trello card ID first (e.g. `TRELLO-004`), then:

```bash
git checkout main
git pull origin main
git checkout -b feature/TRELLO-004-your-description
```

### Make changes and commit

```bash
# After making your changes:
git add .
git commit -m "[TRELLO-004] Brief description of what you did"
```

### Push your branch

```bash
git push origin feature/TRELLO-004-your-description
```

---

## Step 4 — Open a Pull Request (5 min)

1. Go to the repository on GitHub.
2. Click **"Compare & pull request"** on your pushed branch.
3. Title format: `[TRELLO-004] Your description`
4. Add a short description of what changed and why.
5. Submit — CI will run automatically.
6. Wait for the green ✅ before requesting a review.

---

## Step 5 — Troubleshooting

| Problem | Solution |
|---|---|
| `ModuleNotFoundError: flask` | Run `pip install -r requirements.txt` |
| `flake8` reports errors | Fix whitespace/line length issues flagged in output |
| Tests fail locally | Ensure you haven't modified `app.py` unexpectedly |
| CI fails but tests pass locally | Check Python version matches (3.11) |
| Can't push to `main` | `main` is protected — create a feature branch first |
| Merge button greyed out | CI must be green before merging is allowed |

---

## Quick Reference

```bash
# Run app
python app.py

# Run all tests
pytest test_app.py -v

# Run linter
flake8 app.py test_app.py

# Create feature branch
git checkout -b feature/TRELLO-###-description

# Commit with convention
git commit -m "[TRELLO-###] Description"
```
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

**macOS (Homebrew):**
```bash
brew install python@3.11
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3.11 python3-pip -y
```

**Windows:**
Download from [python.org](https://www.python.org/downloads/) and check "Add to PATH".

### Clone & Install

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
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

8 passed in X.XXs
```

Also run the linter to confirm a clean baseline:

```bash
flake8 app.py test_app.py
```

No output = no issues.

---

## Step 3 — Branch Workflow (10 min)

**Never commit directly to `main`.** Always work on a feature branch.

### Create your branch

Find your Trello card ID first (e.g. `TRELLO-004`), then:

```bash
git checkout main
git pull origin main
git checkout -b feature/TRELLO-004-your-description
```

### Make changes and commit

```bash
# After making your changes:
git add .
git commit -m "[TRELLO-004] Brief description of what you did"
```

### Push your branch

```bash
git push origin feature/TRELLO-004-your-description
```

---

## Step 4 — Open a Pull Request (5 min)

1. Go to the repository on GitHub.
2. Click **"Compare & pull request"** on your pushed branch.
3. Title format: `[TRELLO-004] Your description`
4. Add a short description of what changed and why.
5. Submit — CI will run automatically.
6. Wait for the green ✅ before requesting a review.

---

## Step 5 — Troubleshooting

| Problem | Solution |
|---|---|
| `ModuleNotFoundError: flask` | Run `pip install -r requirements.txt` |
| `flake8` reports errors | Fix whitespace/line length issues flagged in output |
| Tests fail locally | Ensure you haven't modified `app.py` unexpectedly |
| CI fails but tests pass locally | Check Python version matches (3.11) |
| Can't push to `main` | `main` is protected — create a feature branch first |
| Merge button greyed out | CI must be green before merging is allowed |

---

## Quick Reference

```bash
# Run app
python app.py

# Run all tests
pytest test_app.py -v

# Run linter
flake8 app.py test_app.py

# Create feature branch
git checkout -b feature/TRELLO-###-description

# Commit with convention
git commit -m "[TRELLO-###] Description"
```

