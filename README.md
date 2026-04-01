# GitOps Workflow & CI Automation

![CI Pipeline](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME/actions/workflows/ci.yml/badge.svg)

A lightweight internal Flask service demonstrating a production-style GitOps workflow
with automated linting, testing, and task tracking via Trello and GitHub Actions.

---

## Project Overview

This project implements a **GitOps-style development workflow** for a small engineering team.
Git acts as the single source of truth. Every change is tracked through Trello, developed on a feature branch, validated by CI automation, and merged only after passing all quality checks.

The application exposes three REST API endpoints:

| Endpoint         | Method | Description                        |
|------------------|--------|------------------------------------|
| `/health`        | GET    | Returns service health status      |
| `/sum`           | POST   | Returns the sum of two numbers     |
| `/reverse-string`| POST   | Returns a reversed string          |

---

## Architecture

```
Trello (Task Tracking)
     │
     ▼
GitHub (Source Control)
  ├── main               ← stable, protected
  └── feature/TRELLO-###-description  ← active development
     │
     ▼
GitHub Actions (CI Pipeline)
  ├── 1. Install Dependencies  (pip install -r requirements.txt)
  ├── 2. Lint Code             (flake8 app.py test_app.py)
  └── 3. Run Tests             (pytest test_app.py -v)
     │
     ▼ (only on green build)
Merge to main via Pull Request
```

---

## Workflow Description

1. A task is created as a card in Trello and assigned a unique ID (e.g. `TRELLO-001`).
2. A feature branch is created: `feature/TRELLO-001-description`.
3. Work is committed using the convention: `[TRELLO-001] Short description`.
4. A Pull Request is opened against `main` — CI runs automatically.
5. If lint or tests fail, the PR is blocked until the build is green.
6. Once CI passes, the PR is reviewed and merged.
7. The Trello card is moved to **Done**.

---

## Commit Convention

All commits must reference a Trello card ID:

```
[TRELLO-###] Short description

Optional longer explanation of what changed and why.
```

**Examples:**
```
[TRELLO-001] Add initial Flask app structure
[TRELLO-002] Add input validation to /sum endpoint
[TRELLO-003] Write API documentation in README
```

---

## Setup Instructions

### Prerequisites
- Python 3.11+
- Git
- pip

### Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the app
python app.py

# 4. Run tests
pytest test_app.py -v

# 5. Run linter
flake8 app.py test_app.py
```

See [GETTING_STARTED.md](./GETTING_STARTED.md) for the full onboarding guide.

---

## Reflection

### 1. What is GitOps and why does it matter for small teams?

<!-- TODO: Write 200–300 words explaining GitOps principles and their value -->

### 2. How does CI automation improve code quality?

<!-- TODO: Write 200–300 words on how linting and automated testing prevent regressions -->

### 3. What challenges did you face implementing this workflow from scratch?

<!-- TODO: Write 200–300 words on your implementation experience -->

### 4. How does the Trello → GitHub → CI chain create accountability?

<!-- TODO: Write 200–300 words on traceability from task to merged code -->

### 5. What would you change or add if this were a real production system?

<!-- TODO: Write 200–300 words on improvements: Docker, environments, coverage, etc. -->

---

## License

MIT
