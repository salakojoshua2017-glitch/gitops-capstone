# Contributing Guide

This document defines the full development workflow for this project.
All contributors — including solo developers — must follow these standards.

---

## Development Workflow

```
1. Pick a Trello card  →  move to "In Progress"
2. Create a feature branch from main
3. Write code + tests
4. Lint locally (flake8)
5. Test locally (pytest)
6. Push branch
7. Open Pull Request
8. CI runs automatically
9. Fix any failures
10. Merge on green CI
11. Move Trello card to "Done"
```

---

## Branching Rules

| Branch | Purpose | Direct Push Allowed |
|---|---|---|
| `main` | Stable, production-ready code | ❌ Never |
| `feature/TRELLO-###-*` | All active development | ✅ Yes |

### Branch naming format:

```
feature/TRELLO-###-short-description
```

**Examples:**
```
feature/TRELLO-001-initial-setup
feature/TRELLO-002-input-validation
feature/TRELLO-005-add-palindrome-test
```

Rules:
- Always branch off the latest `main`
- One Trello card = one branch
- Delete branches after merging

---

## Commit Format

Every commit **must** reference a Trello card:

```
[TRELLO-###] Short imperative description

Optional body — explain what changed and why.
Wrap lines at 72 characters.
```

**Good commits:**
```
[TRELLO-001] Add initial Flask app and project structure
[TRELLO-002] Add flake8 lint step to CI pipeline
[TRELLO-003] Write onboarding guide in GETTING_STARTED.md
```

**Bad commits (will be rejected in review):**
```
fix stuff
updated file
wip
```

---

## Pull Request Process

1. **Title** must follow: `[TRELLO-###] Description`
2. **Description** must include:
   - What was changed
   - Why it was changed
   - How to test it
3. Link the Trello card in the PR description
4. CI must be **green** before merging
5. At least one approval required (for team setups)
6. Squash or merge commit — no force pushes to `main`

---

## CI/CD Explanation

The pipeline runs on every push and pull request via GitHub Actions.

**File:** `.github/workflows/ci.yml`

### Pipeline stages (in order):

```
Stage 1: Install Dependencies
└── pip install -r requirements.txt

Stage 2: Lint Code
└── flake8 app.py test_app.py
    ├── Fails on: lines > 79 chars, unused imports,
    │             missing whitespace, syntax errors
    └── A lint failure = RED build = PR blocked

Stage 3: Run Tests
└── pytest test_app.py -v
    ├── All 8 tests must pass
    └── A test failure = RED build = PR blocked
```

### Triggers:
- Push to `main`
- Push to any `feature/**` branch
- Pull request targeting `main`

---

## Coding Standards

This project follows **PEP 8** enforced by `flake8`.

Key rules:
- Max line length: **79 characters**
- 2 blank lines between top-level functions
- 1 blank line between methods inside a class
- No trailing whitespace
- No unused imports
- Use `snake_case` for variables and functions

Run before every commit:
```bash
flake8 app.py test_app.py
```

---

## Failure Handling

### Lint failure
```bash
# See exactly what flake8 is complaining about
flake8 app.py test_app.py

# Fix the flagged lines, then re-commit
git add .
git commit -m "[TRELLO-###] Fix flake8 lint errors"
git push
```

### Test failure
```bash
# Run tests locally with verbose output
pytest test_app.py -v

# Identify the failing test, fix the code, re-run
# Never modify tests to make them pass — fix the code
```

### CI failure on PR
- Do **not** merge with a failing build
- Push a fix commit to the same branch — CI re-runs automatically
- Tag a teammate if you're stuck

---

## Trello Card Lifecycle

```
Backlog → In Progress → Review/QA → Done
```

- Move card to **In Progress** when you create the branch
- Move to **Review/QA** when the PR is opened
- Move to **Done** only after the PR is merged

