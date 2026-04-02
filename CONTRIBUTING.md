# Contributing Guide

This document defines the full development workflow for this project.
All contributors must follow these standards without exception.

---

## Development Workflow
```
1. Pick a Trello card       →  move to In Progress
2. Create a feature branch  →  from latest main
3. Write code and tests
4. Lint locally             →  flake8 app.py test_app.py
5. Test locally             →  pytest test_app.py -v
6. Push branch              →  git push origin feature/...
7. Open Pull Request        →  title must include Trello ID
8. CI runs automatically    →  must be green to merge
9. Merge on green CI        →  squash or merge commit
10. Move Trello card        →  to Done
```

---

## Branching Rules

| Branch | Purpose | Direct Push |
|---|---|---|
| main | Stable, production-ready | Never |
| feature/TRELLO-###-* | All active development | Yes |

### Branch naming:
```
feature/TRELLO-###-short-description
```

Examples:
```
feature/TRELLO-001-initial-setup
feature/TRELLO-004-documentation
feature/TRELLO-005-onboarding-guide
```

Rules:
- Always branch off the latest main
- One Trello card = one branch
- Delete branches after merging

---

## Commit Format

Every commit must reference a Trello card:
```
[TRELLO-###] Short imperative description

Optional body explaining what changed and why.
Wrap lines at 72 characters.
```

Good commits:
```
[TRELLO-001] Add initial Flask app and project structure
[TRELLO-002] Add GitHub Actions CI pipeline
[TRELLO-003] Fix indentation errors in app.py and test_app.py
```

Bad commits:
```
fix stuff
updated file
wip
asdfgh
```

---

## Pull Request Process

1. Title must follow: [TRELLO-###] Description
2. Description must include what changed, why, and how to test
3. CI must be green before merging
4. No force pushes to main ever

---

## CI/CD Explanation

File: .github/workflows/ci.yml

Pipeline runs on every push and pull request.
```
Stage 1: Install Dependencies
         pip install -r requirements.txt

Stage 2: Lint Code
         flake8 app.py test_app.py
         Fails on: lines over 79 chars, unused imports,
         bad whitespace, syntax errors

Stage 3: Run Tests
         pytest test_app.py -v
         All 8 tests must pass
```

A failure at any stage blocks the PR from merging.

---

## Coding Standards

This project follows PEP 8 enforced by flake8:
- Max line length: 79 characters
- 2 blank lines between top-level functions
- No trailing whitespace
- No unused imports
- snake_case for all variables and functions

---

## Failure Handling

### Lint failure
```bash
flake8 app.py test_app.py   # see exact errors
# fix flagged lines
git add .
git commit -m "[TRELLO-###] Fix flake8 lint errors"
git push
```

### Test failure
```bash
pytest test_app.py -v   # identify failing test
# fix the code, never modify tests to force a pass
```

### Push rejected
```bash
git pull origin main --rebase
git push origin your-branch
```

---

## Trello Card Lifecycle
```
Backlog → In Progress → Review/QA → Done
```

- In Progress  →  when you create the branch
- Review/QA    →  when the PR is opened
- Done         →  only after the PR is merged
