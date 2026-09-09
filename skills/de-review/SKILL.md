---
name: de-review
description: Review selected changes and remove unnecessary abstractions through verified ablation experiments.
disable-model-invocation: true
---

# De-review

Review one pinned change set with `$code-review` and `$ponytail-review`, then apply only simplifications that an ablation shows are safe.

## Pin the change set

1. Capture `git status --short`, then select one scope:
   - A user-supplied commit or range takes priority. Resolve every revision first. Compare a single commit with its parent, compare a contiguous range at its boundaries, and inspect non-contiguous commits as separate patches. Do not widen the selection to `HEAD`.
   - An explicit staged request uses `git diff --cached` and excludes unstaged and untracked changes.
   - An explicit unstaged request uses `git diff` and treats untracked files as complete additions while excluding index-only changes.
   - Otherwise, review all uncommitted changes with `git diff HEAD` and treat each untracked file as a complete addition.
2. Stop when the selected change set is empty. Record the exact commands, revisions, and paths so every review pass uses the same snapshot.

## Review before editing

1. Run `$code-review` and `$ponytail-review` against the pinned snapshot. For worktree or exact-commit scopes, replace `$code-review`'s default `<fixed-point>...HEAD` command with the pinned commands while keeping its Standards and Spec axes unchanged.
2. Use the user's request as the spec when it states the required behavior. Otherwise, follow `$code-review`'s spec search. If no source exists, mark Spec as unavailable instead of inventing requirements.
3. Keep the Standards, Spec, and Ponytail findings separate. Use only unnecessary complexity introduced by the selected change set as ablation candidates. Exclude explicit requirements and behavior needed for correctness, security, compatibility, accessibility, or data-loss prevention.

## Run ablations

1. Choose an experiment tree. Use the current working tree when it matches the pinned snapshot; otherwise, copy the pinned content to a temporary location and remove it after the experiments.
2. Establish a baseline with the smallest repository-native checks that cover the changed behavior. Record pre-existing failures. Trace every caller and requirement that depends on each candidate because unchanged tests prove only the behavior they cover.
3. Test one candidate at a time:
   - State the hypothesis: what can be removed, what replaces it, and which behavior must remain.
   - Apply the smallest removal or replacement in the experiment tree, then run the baseline and focused checks and inspect affected callers.
   - Keep the ablation only when required behavior remains, no new failure appears, and production code, dependencies, or design concepts decrease. If the result fails or remains uncertain, reverse only that experiment's hunks.
4. Treat each accepted ablation as the next baseline. When using a temporary copy, apply accepted hunks to the current working tree only when they still match.
5. Rerun the relevant checks and inspect the complete task-owned diff. Leave the index and Git history unchanged unless the user asks otherwise.

## Report

Report the pinned scope and keep `Standards`, `Spec`, and `Ponytail` separate. For each ablation, list its result, evidence, and net reduction. Include final checks and Git state. If no candidate passes, leave the code unchanged.
