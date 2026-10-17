# Git & GitHub Workflow Rules

This document establishes the mandatory Git, GitHub, identity, and contribution integrity rules for this repository and agent sessions.

---

## 1. Session Start Verification (Mandatory)

Before executing or proposing any file modifications or commits:
1. **Verify Git Identity (Local Config Only)**:
   - Confirm local repository config:
     ```bash
     git config --local user.name
     git config --local user.email
     ```
   - Must match authorized identity:
     - `user.name`: `dkayush7373`
     - `user.email`: `dkayush73@gmail.com`
   - If not set locally, configure immediately with `--local` (never `--global`):
     ```bash
     git config --local user.name "dkayush7373"
     git config --local user.email "dkayush73@gmail.com"
     ```
   - Confirm via `git config --show-origin --get user.email` that the config source is `file:.git/config`.

2. **Verify Repository & Remote State**:
   - Inspect top-level directory: `git rev-parse --show-toplevel`
   - Inspect branch and sync status: `git status --short --branch`
   - Inspect remotes: `git remote -v`
   - Verify remote connectivity: `git ls-remote --heads origin`
   - Identify active/default branch and whether submodules or nested repositories exist.

---

## 2. Commit After Every Logical Step (No Mega-Commits)

Do **not** batch entire multi-task sessions or whole projects into a single commit.
For each completed feature, fix, refactor, test suite, or documentation update:
1. **Complete the logical step**: Ensure the code unit is complete and functional.
2. **Run Quality Gates**:
   - Run linting: `npm run lint` (or project equivalent)
   - Run typechecking: `npx tsc --noEmit` (or project equivalent)
   - Run test suite: `npm test` or `npm run test`
   - Resolve any errors introduced before staging.
3. **Inspect Diff**:
   - Review working directory changes: `git status`
   - Review exact diff: `git diff`
4. **Explicit Staging**:
   - Stage ONLY intended files explicitly by path (`git add <file1> <file2>`).
   - Never use blind `git add .` or `git add -A`.
5. **Conventional Commit**:
   - Craft a precise conventional commit message:
     - `feat(scope): ...`
     - `fix(scope): ...`
     - `test(scope): ...`
     - `refactor(scope): ...`
     - `docs(scope): ...`
     - `chore(scope): ...`
   - Never create empty, placeholder, or per-keystroke commits.
6. **Verify Commit Locally**:
   - Verify author and commit SHA:
     ```bash
     git log -1 --format="%H | %an | %ae | %s"
     ```
   - Confirm `%ae` is `dkayush73@gmail.com` and `%an` is `dkayush7373`.
7. **Push Directly to Default Branch (`main`)**:
   - Push to default branch: `git push origin main`
   - Commits must reside directly on the default branch (`main`) to immediately trigger contribution graph updates. Never leave commits solely on feature branches.
8. **Verify Remotely**:
   - Compare local HEAD with remote branch tip:
     ```bash
     git rev-parse HEAD
     git ls-remote origin main
     ```
   - Record full 40-character SHA and commit URL:
     `https://github.com/<owner>/<repo>/commit/<FULL_SHA>`

---

## 3. Strict Safety Invariants

- **No History Rewrites**: Never run `--amend`, `rebase`, `reset --hard`, or force-push (`--force`) without explicit user instruction.
- **Never Rewrite History for Past Attribution**: If past commits have incorrect emails, never alter git history unilaterally.
- **Zero Secrets**: Never commit `.env`, `.env.local`, API keys, private tokens, passwords, or build artifacts. Verify against `.gitignore`.
- **Preserve User Changes**: Never overwrite or discard unstaged work from the user.
- **No Squash Merges**: Never squash-merge or recommend squash merges, as squash merges collapse distinct commits into a single commit and erase individual contributions. Use fast-forward merges, merge commits, or direct pushes to `main`.
- **Halt on Ambiguity**: On any merge conflict, auth failure, remote mismatch, or ambiguous repository state, stop execution immediately and report with full diagnostic output.

---

## 4. GitHub Contribution Integrity & Truthfulness

- GitHub contribution graphs only increment when:
  1. The author email (`%ae`) exactly matches an email confirmed in GitHub Account Settings (`https://github.com/settings/emails`).
  2. The commit is pushed to the default branch (e.g. `main`) or `gh-pages` in a standalone repository or merged PR.
  3. "Keep my email addresses private" is not blocking attribution or masking the address.
- Never claim the contribution graph increased. Contribution metrics are cached server-side on GitHub and can take up to 24 hours to re-index.
- Never invent commit SHAs, test results, remote URLs, or contribution counts. Always provide real terminal outputs and verifiable evidence.

