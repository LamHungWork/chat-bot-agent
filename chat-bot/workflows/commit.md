---
description: Automated git commit workflow following Conventional Commits standards.
---

# Git Commit Workflow

This workflow analyzes staged changes and creates a semantic git commit message.

## 1. Analyze Changes

- **Status Check**: Run `git status --short` to see what files are changed.
- **Diff Summary**: Run `git diff --staged --stat` to understand the scale of changes.
- **Detailed Diff (Optional)**: ONLY if the summary is insufficient, run `git diff --staged` to read specific changes.

## 2. Generate Message

- **Format**: `<type>(<scope>): <subject>`
- **Types**:
  - `feat`: New features
  - `fix`: Bug fixes
  - `refactor`: Code restructuring
  - `test`: Adding/fixing tests
  - `chore`: Maintenance/Config
  - `docs`: Documentation changes
- **Rules**:
  - Subject: Max 72 chars, imperative mood ("add" not "added"), lowercase, no period.
  - Scope: Unstyled module name (e.g., `auth`, `api`).
  - Body: Omit unless strictly necessary for breaking changes.

## 3. Execute Commit

- **Approval**: Show the generated command to the user first? -> **NO**, as per "turbo" annotations below, we can auto-run if confident. However, for commit messages, it is best practice to propose the command `git commit -m "..."` via `run_command` and let the user approve it in the UI.

## 4. Workflow Steps

1. Check current status.

   ```bash
   git status --short
   ```

2. Check staged diff summary.

   ```bash
   git diff --staged --stat
   ```

3. Construct the commit command and propose it to the user.
   - Example: `git commit -m "feat(agent): implement rude persona logic"`

> [!IMPORTANT]
> If nothing is staged (`git diff --staged` is empty), ask the user if they want to stage all changes (`git add .`) first.
