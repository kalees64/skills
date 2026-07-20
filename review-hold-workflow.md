---
name: review-hold-workflow
description: Performs project changes inside a Git-backed review-hold workflow. Apply edits, then let the user accept or reject changes, with editor-based diffs and per-file review. Use this skill whenever the user asks to change project files and wants reviewable, reversible edits.
tags: [git, review, approval, workflow, vscode]
---

# Review-Hold Workflow

This skill enforces a Git-backed accept/reject workflow so project edits are always inspectable and reversible. It is intended for the assistant to follow when modifying files in user projects.

## Defaults and Preferences

- Editor: VS Code / VSCodium (`code`)
- Diff style: editor/formatted diff, not raw terminal output
- Include only changed files in review; omit untouched files
- Highlight additions and deletions distinctly
- Review is per file, not whole-change only
- Do not silently overwrite project files

## When to Use

- The user asks to change project files
- The user explicitly requests "accept/reject", "review changes", "hold for review", or similar
- Any non-trivial file modification in a Git project

## Workflow

### 1. Verify Git project

Confirm the target directory is a Git repo:
- `git rev-parse --show-toplevel`
If not a Git repo, notify the user and ask whether to initialize Git before proceeding.

### 2. Create review branch

Create a dedicated review branch for this change set.

Preferred branch name: `review-hold/<short-description>` or `review-hold/<timestamp>`

Commands:
- `git checkout -b review-hold/<name>`
- `git add -A`
- `git commit -m "review-hold: snapshot before applying <description>"`

This preserves the original state and gives the user a clean reference.

### 3. Apply changes

Make the requested edits in the review branch only. Keep changes isolated and minimal. Avoid unrelated modifications.

### 4. Stage review

After edits are complete:

- Run `git add -A`
- Optionally run `git diff --cached --name-only` to list changed files

### 5. Present review in VS Code

Open VS Code diff review against the original branch.

Preferred commands:
- `code --diff <original-file-path> <review-branch-file-path>`
- Or open the repo with `code <repo>` and use Source Control diff view

Show the user:
- A short summary of what changed
- The list of changed files
- That they can review visually in VS Code

If VS Code is unavailable, fall back to the terminal review format:
- Show changed files only
- Show colored additions/removals
- Omit untracked files unrelated to this task

### 6. Per-file accept/reject

Ask the user for their decision for each changed file.

Accepting a file:
- Keep the change
- `git checkout main -- <file>` is NOT used; instead keep the file as-is on the review branch

Rejecting a file:
- Revert to the original state from main before review began
- `git checkout main -- <file>` from the review branch

After each decision, summarize the remaining accepted files.

### 7. Finalize

Once the user is done:

If at least one file is accepted:
- Offer to merge the review branch back to main: `git checkout main && git merge --no-ff review-hold/<name>`
- Or leave the branch for the user to review in a PR

If all files are rejected:
- `git checkout main`
- `git branch -D review-hold/<name>`
- Report that no changes were kept

### 8. Cleanup

Delete the review branch only after the user confirms merge or explicit rejection of all changes.

Do not force-push or rewrite public history unless the user requests it.

## Example Session

User: "Add error handling to the API fetch in src/api.ts"

Assistant:
1. `git rev-parse --show-toplevel`
2. `git checkout -b review-hold/api-fetch-error-handling`
3. `git add -A && git commit -m "review-hold: pre-change snapshot"`
4. Edit `src/api.ts`
5. `git add src/api.ts`
6. `code --diff src/api.ts src/api.ts`
7. Ask: "Accept changes to `src/api.ts`? (accept/reject)"
8. On accept: keep file
   On reject: `git checkout main -- src/api.ts`
9. `git checkout main && git merge --no-ff review-hold/api-fetch-error-handling`

## Fail State Recovery

If a review branch is abandoned mid-way:
- Uncommitted changes in the worktree should be stashed or committed before switching branches
- Recover by checking for uncommitted changes: `git status --short`
- If needed: `git checkout main && git checkout -- .`

## Rules

1. Always use a dedicated review branch for project changes.
2. Never edit project files outside the review branch.
3. Always present changes visually or in formatted diff, not raw terminal dumps.
4. Show only changed files; omit untouched files.
5. Allow per-file accept/reject decisions.
6. Do not delete work without explicit user confirmation.
