# GitOps Workflow & CI Automation

A lightweight internal Flask service demonstrating a production-style GitOps workflow
with automated linting, testing, and task tracking via Trello and GitHub Actions.

---

## Project Overview

This project implements a GitOps-style development workflow for a small engineering team.
Git acts as the single source of truth. Every change is tracked through Trello, developed
on a feature branch, validated by CI automation, and merged only after passing all quality
checks.

The application exposes three REST API endpoints:

| Endpoint          | Method | Description                    |
|-------------------|--------|--------------------------------|
| `/health`         | GET    | Returns service health status  |
| `/sum`            | POST   | Returns the sum of two numbers |
| `/reverse-string` | POST   | Returns a reversed string      |

---

## Architecture
```
Trello (Task Tracking)
     │
     ▼
GitHub (Source Control)
  ├── main                          ← stable, protected
  └── feature/TRELLO-###-description  ← active development
     │
     ▼
GitHub Actions (CI Pipeline)
  ├── 1. Install Dependencies
  ├── 2. Lint Code (flake8)
  └── 3. Run Tests (pytest)
     │
     ▼ (only on green build)
Merge to main via Pull Request
```

---

## Workflow Description

1. A task is created as a card in Trello with a unique ID (e.g. TRELLO-001).
2. A feature branch is created: feature/TRELLO-001-description.
3. Work is committed using the convention: [TRELLO-001] Short description.
4. A Pull Request is opened against main — CI runs automatically.
5. If lint or tests fail, the PR is blocked until the build is green.
6. Once CI passes, the PR is reviewed and merged.
7. The Trello card is moved to Done.

---

## Commit Convention

All commits must reference a Trello card ID:
```
[TRELLO-###] Short imperative description

Optional longer explanation of what changed and why.
```

Examples:
```
[TRELLO-001] Add initial Flask app structure
[TRELLO-002] Add CI pipeline with GitHub Actions
[TRELLO-003] Fix indentation errors in app.py and test_app.py
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
git clone https://github.com/salakojoshua2017-glitch/gitops-capstone.git
cd gitops-capstone

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the app
python app.py

# 4. Run tests
pytest test_app.py -v

# 5. Run linter
flake8 app.py test_app.py
```

See GETTING_STARTED.md for the full onboarding guide.

---

## Reflection

### 1. What is GitOps and why does it matter for small teams?

GitOps is a modern operational framework that uses Git as the single source of truth
for both application code and infrastructure configuration. Instead of manually applying
changes to systems, every change is made through a Git commit, reviewed via a pull
request, and automatically applied through automation pipelines. For small teams, GitOps
matters because it brings structure and discipline to workflows that might otherwise be
chaotic. Without GitOps, small teams often rely on verbal agreements, undocumented
processes, and direct changes to production environments — all of which introduce risk.
With GitOps, every change is traceable, reversible, and auditable. If something breaks,
you can look at the Git history and immediately identify what changed, when, and who
made the change. For a team of one to three developers, this is invaluable because there
is no bureaucracy to fall back on — the process itself becomes the safety net. GitOps also
enables asynchronous collaboration, meaning team members do not need to be online at
the same time to review and approve changes. The pull request becomes the conversation,
and the CI pipeline becomes the automated quality gate. This project demonstrates GitOps
by linking every commit to a Trello task, enforcing quality through GitHub Actions, and
requiring all changes to go through a pull request before reaching main.

### 2. How does CI automation improve code quality?

Continuous Integration automation improves code quality by removing the human element
from quality enforcement. Without CI, a developer might forget to run tests before pushing,
or might not have flake8 installed locally, allowing broken or poorly formatted code to
reach the main branch. With CI, every push and pull request automatically triggers a
pipeline that installs dependencies, lints the code with flake8, and runs the full test
suite with pytest. This means no code can reach main without passing all quality checks,
regardless of the developer's local setup. In this project, flake8 enforces PEP 8 style
rules — catching issues like lines that are too long, missing whitespace, unused imports,
and indentation errors before they become technical debt. Pytest then validates that all
eight test cases pass, ensuring the application behaves correctly after every change. CI
also creates a feedback loop that helps developers improve over time. When a build fails,
the developer sees exactly which line caused the issue and fixes it immediately, rather
than discovering the bug days later during a code review or in production. This project
required fixing real lint and indentation errors during setup, which demonstrated
precisely how CI catches issues that are easy to overlook manually.

### 3. What challenges did you face implementing this workflow from scratch?

Implementing this workflow from scratch presented several practical challenges. The first
was file encoding — copying files from Windows into WSL introduced CRLF line endings
that corrupted the YAML workflow file, preventing GitHub Actions from recognising it.
This required recreating files directly in the WSL terminal using the cat heredoc method
to ensure clean LF line endings. The second challenge was file content corruption — using
the cat command incorrectly caused app.py to have its content duplicated, introducing
undefined names and redefined imports that caused flake8 to fail. Reading the exact error
messages in the GitHub Actions logs was essential to diagnosing and fixing this quickly.
The third challenge was Git history synchronisation — deleting the ci.yml file directly
on GitHub created a remote commit that was not present locally, causing the next push to
be rejected. Resolving this required using git pull --rebase to replay local commits on
top of the remote changes cleanly. Each of these challenges reinforced the importance of
understanding the tools at a low level, not just following steps. A DevOps engineer must
be able to read error messages, reason about what went wrong, and apply the correct fix
without breaking the existing history.

### 4. How does the Trello → GitHub → CI chain create accountability?

The Trello to GitHub to CI chain creates a complete audit trail that connects every line
of code back to a business decision. It starts with a Trello card, which represents a
defined piece of work with a title, description, and unique ID. When a developer picks
up that card and moves it to In Progress, they create a feature branch named after the
card ID. Every commit on that branch references the same ID in its message, making it
possible to search the Git log and immediately find all commits related to a specific task.
When the developer opens a pull request, the CI pipeline runs automatically and either
approves or blocks the merge based on objective quality criteria — not opinion. This means
accountability is built into the workflow at every stage. If a bug is introduced, you can
trace it to a specific PR, a specific commit, and a specific Trello card. If a card was
never completed, the Git log will show no commits referencing that ID. This chain also
creates accountability for process compliance — if a developer pushes directly to main or
uses a commit message without a Trello ID, it is immediately visible in the history as a
deviation from the agreed workflow. For a small team without a dedicated QA department,
this kind of structured traceability is what separates a professional engineering team
from an informal group of developers.

### 5. What would you change or add if this were a real production system?

If this were a real production system, several improvements would significantly increase
its robustness and reliability. First, I would add branch protection rules on GitHub to
enforce that no direct pushes to main are possible and that at least one reviewer must
approve a pull request before merging. This ensures the process is enforced technically,
not just by convention. Second, I would containerise the application using Docker so that
the environment is identical across development, CI, and production — eliminating the
class of bugs caused by environment differences. Third, I would add test coverage
reporting using pytest-cov and set a minimum coverage threshold in the CI pipeline, so
that new code cannot be merged without adequate test coverage. Fourth, I would implement
separate workflow environments for development, staging, and production, with different
automated checks at each stage. Fifth, I would integrate secret scanning and dependency
vulnerability checking into the CI pipeline using tools like GitHub's Dependabot or
Trivy. Finally, I would add automated deployment steps so that a successful merge to main
automatically deploys the application to a staging environment, completing the CD half of
a full CI/CD pipeline. These additions would transform this proof-of-concept workflow
into a production-grade GitOps system.

---

## License

MIT
