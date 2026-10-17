# AGENTS.md — Workspace Git & Engineering Rules

This repository enforces strict Git hygiene, authorship attribution, and quality gates for all agent interactions.

---

## 1. Identity Verification at Session Start

1. Local Git identity must be explicitly configured and verified:
   - `git config --local user.name "dkayush7373"`
   - `git config --local user.email "dkayush73@gmail.com"`
2. Verify via:
   - `git config --show-origin --get user.name`
   - `git config --show-origin --get user.email`
   - Both must point to `file:.git/config`.

---

## 2. Commit Discipline: Logical Steps

- **No Mega-Commits**: Every distinct feature, fix, refactor, or configuration change must be committed as its own logical unit.
- **Quality Gates First**:
  - Run linting: `npm run lint`
  - Run typechecking: `npx tsc --noEmit`
  - Run tests: `npm test`
- **Explicit Staging**:
  - `git add <exact-path>` (no blind `git add .`).
- **Conventional Commits**:
  - Standard format: `type(scope): description`.
- **Remote Push & Verification**:
  - Commit locally, push to upstream branch, and verify with `git ls-remote origin <branch>`.
  - Record the commit hash and URL: `https://github.com/<owner>/<repo>/commit/<SHA>`.

---

## 3. Safety Invariants

- Never run `--amend`, squash, `rebase`, `reset --hard`, or force-push without explicit permission.
- Never rewrite history to fix past commit attributions without authorization.
- Never commit credentials, `.env` files, or build artifacts.
- Never overwrite uncommitted user changes.
- In case of conflicts, authentication issues, or ambiguity: stop and report immediately.

---

## 4. GitHub Contribution Integrity

- Commits must use the verified email associated with the GitHub account (`dkayush73@gmail.com`).
- Commits must reside on the default branch (or be merged into it) in a recognized repository.
- Contribution graph updates can take up to 24 hours to reflect on GitHub profile pages.
