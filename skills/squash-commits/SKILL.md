---
name: squash-commits
description: Rebase the current Git branch onto its default integration branch, then squash its commits into one while preserving the rebased tree.
disable-model-invocation: true
---

# Squash Commits

Rebase the current branch onto its integration branch, then replace the branch commits with one summarized commit.

## Inspect

1. Read the repository instructions.
2. Require a clean worktree, a named current branch, and no Git operation in progress. Record the branch as `original_branch` and `HEAD^{commit}` as `original_oid`.
3. Use a base ref supplied by the user. Otherwise, identify the repository's default integration branch from repository instructions or a configured remote's symbolic `HEAD`, such as `refs/remotes/<remote>/HEAD`.
4. If the evidence does not select exactly one base ref, ask the user for it and wait for an answer. Do not infer `main` or `master` from its name alone.
5. Resolve `base_ref^{commit}` as `base_oid`. If it does not resolve to a commit, ask the user for a valid base ref and wait for an answer.
6. Create a uniquely named local backup branch at `original_oid`, such as `backup/squash-commits-<timestamp>`. Record its name as `backup_branch`, resolve it as `backup_oid`, and require `backup_oid` to equal `original_oid`.
7. Recheck that the current branch, HEAD, and clean worktree still match the recorded starting state. If they changed, preserve the new state, report it with the backup branch, and stop. Otherwise, run `git rebase "$base_oid"`. If it fails, use **Restore**, report the failure, and stop.
8. Record the rebased `HEAD` as `rebased_oid` and require `base_oid` to be its ancestor.
9. Count `base_oid..HEAD`. If it contains zero or one commit, report that no squash is needed, including the rebase result and backup branch, and stop.

Do not fetch, push, or create a pull request unless the user separately requests it.

## Restore

Use this recovery path whenever rebase, any squash step, or verification fails after the backup exists:

Before aborting or resetting, compare the current branch, HEAD, index, and worktree with the recorded state and expected effects of the last attempted command. If new user commits, edits, hook changes, or unexplained differences are present, preserve them and the backup, report the repository state, and stop. An initially clean worktree does not authorize discarding later work.

1. If a rebase is in progress, run `git rebase --abort`. If abort fails or any Git operation remains in progress, report the exact repository state and stop without further mutation.
2. Require the current branch to equal `original_branch`. If it does not, report the exact repository state and stop without moving another branch.
3. Run `git reset --hard "$backup_oid"` only after the recovery checks above establish that it discards changes from this operation and `backup_branch^{commit}` still equals `backup_oid`.
4. Require `HEAD` and `backup_branch^{commit}` to equal `backup_oid`, `git status --porcelain` to be empty, and no Git operation to remain in progress.
5. Report the failed step, restoration result, and backup branch, then stop.

## Summarize

Inspect the complete branch change and its original commits:

- `git log --reverse base_oid..HEAD`
- `git diff --stat base_oid..HEAD`
- `git diff base_oid..HEAD`
- recent repository commits for message conventions

Compose one message for the net result:

- Follow the repository's established format.
- Use a concise imperative subject, preferably no more than 72 characters.
- Add a body only when it helps explain the main changes or motivation.
- Preserve existing user-facing issue references and breaking-change notes.
- Preserve existing provenance and compliance trailers such as `Co-authored-by` and `Signed-off-by`; never invent trailers.
- Omit review-only trailers and per-commit identifiers such as `Reviewed-by` and `Change-Id`, unless repository instructions require them on the squashed commit.
- Use `git interpret-trailers --parse` when needed to distinguish trailers from body text.
- Omit fixup chronology, review iterations, and references to squashing.

## Squash

If any step in this section fails, use **Restore** and stop.

1. Require the current branch to equal `original_branch`, the worktree to be clean, and HEAD to equal `rebased_oid`. If the state changed, preserve it, report the backup branch, and stop. Otherwise, record `git rev-parse HEAD^{tree}` as `expected_tree`.
2. Run `git reset --soft "$base_oid"`.
3. Confirm the staged change is non-empty.
4. Commit non-interactively with the summarized message.

## Verify

Require all checks to pass:

- `git rev-list --count "$base_oid..HEAD"` returns `1`.
- `git rev-parse HEAD^` equals `base_oid`.
- `git rev-parse HEAD^{tree}` equals `expected_tree`.
- `git status --porcelain` is empty.

If verification fails, use **Restore**. Otherwise, report the selected base ref and OID, rebase result, new commit OID and message, verification result, and backup branch.
