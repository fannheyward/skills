---
name: squash-commits
description: Rebase the current Git branch onto its default integration branch, then squash its commits into one while preserving the rebased tree.
disable-model-invocation: true
---

# Squash Commits

Rebase the current branch onto its integration branch, then replace the branch commits with one summarized commit.

## Inspect

1. Read the repository instructions.
2. Require a clean worktree, a named current branch, and no Git operation in progress.
3. Use a base ref supplied by the user. Otherwise, identify the repository's default integration branch from repository instructions or a configured remote's symbolic `HEAD`, such as `refs/remotes/<remote>/HEAD`.
4. If the evidence does not select exactly one base ref, ask the user for it and wait for an answer. Do not infer `main` or `master` from its name alone.
5. Resolve `base_ref^{commit}` as `base_oid`. If it does not resolve to a commit, ask the user for a valid base ref and wait for an answer.
6. Create a uniquely named local backup branch at the original `HEAD`, such as `backup/squash-commits-<timestamp>`.
7. Run `git rebase "$base_oid"`. If it fails, run `git rebase --abort`, confirm `HEAD` equals the backup branch and the worktree is clean, report the conflict, and stop.
8. Require `base_oid` to be an ancestor of the rebased `HEAD`.
9. Count `base_oid..HEAD`. If it contains zero or one commit, report that no squash is needed, including the rebase result and backup branch, and stop.

Do not fetch, push, or create a pull request unless the user separately requests it.

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
- Preserve supported issue references, breaking-change notes, and co-author trailers.
- Omit fixup chronology, review iterations, and references to squashing.

## Squash

1. Record `git rev-parse HEAD^{tree}` as `expected_tree`.
2. Run `git reset --soft "$base_oid"`.
3. Confirm the staged change is non-empty.
4. Commit non-interactively with the summarized message.

## Verify

Require all checks to pass:

- `git rev-list --count "$base_oid..HEAD"` returns `1`.
- `git rev-parse HEAD^` equals `base_oid`.
- `git rev-parse HEAD^{tree}` equals `expected_tree`.
- `git status --porcelain` is empty.

If verification fails, restore the original branch from the backup. Otherwise, report the selected base ref and OID, rebase result, new commit OID and message, verification result, and backup branch.
