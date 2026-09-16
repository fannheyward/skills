---
name: de-review
description: Review selected changes and remove unnecessary abstractions through verified ablation experiments.
disable-model-invocation: true
---

# De-review

Review one pinned change set with `$review-agent`, `$code-review`, and `$ponytail-review`, then apply only simplifications that an ablation shows are safe.

An explicit review-only request limits this workflow to findings. If the user asks to confirm a plan, present the candidates before editing. Otherwise, complete the supported ablations within the selected scope.

## Pin the change set

1. Capture `git status --short`, then select one scope:
   - A user-supplied commit or range takes priority. Resolve every revision first. Compare a single commit with its parent, compare a contiguous range at its boundaries, and inspect non-contiguous commits as separate patches. Do not widen the selection to `HEAD`.
   - An explicit staged request uses `git diff --cached` and excludes unstaged and untracked changes.
   - An explicit unstaged request uses `git diff` and treats untracked files as complete additions while excluding index-only changes.
   - Otherwise, review all uncommitted changes with `git diff HEAD` and treat each untracked file as a complete addition.
2. Stop when the selected change set is empty. Record the exact commands, resolved revisions, paths, and selected file contents so every pass uses the same snapshot. Preserve the initial index and worktree state for detecting later edits.

## Review before editing

1. Run `$review-agent` for actionable defects, `$code-review` for Standards and Spec, and `$ponytail-review` for unnecessary complexity against the pinned snapshot. Pass the recorded commands, revisions, paths, and file contents to every pass. These override each skill's default diff selection, including `$review-agent`'s base-branch comparison and `$code-review`'s `<fixed-point>...HEAD` command.
2. Use the user's request as the spec when it states the required behavior. Otherwise, search issue references and relevant repository specs with available tools. A missing issue-tracker setup file does not block review. If no source is available, mark Spec as unavailable and continue the supported axes.
3. Keep review agents read-only. Delegate `$review-agent` to a separate agent and use parallel Standards and Spec reviews when the active agent policy permits, respecting its role and concurrency limits. If a referenced skill or independent agent is unavailable, disclose the missing stage and perform the supported review in the primary agent; do not claim an independent pass or install tooling to obtain one.
4. Keep the Defects, Standards, Spec, and Ponytail findings separate. Use only unnecessary complexity introduced by the selected change set as ablation candidates. Exclude explicit requirements and behavior needed for correctness, security, compatibility, accessibility, or data-loss prevention.

## Run ablations

1. Choose an experiment tree. Use the current working tree when it matches the pinned snapshot; otherwise, copy the pinned content to a temporary location and remove it after the experiments.
2. Establish a baseline with the smallest repository-native checks that cover the changed behavior. Reuse existing results for identical content and check configuration. Record pre-existing failures. Trace the callers and requirements affected by each candidate because unchanged tests prove only the behavior they cover. If required validation cannot run, report the candidate as unverified and leave it unapplied.
3. Test one candidate at a time:
   - State the hypothesis: what can be removed, what replaces it, and which behavior must remain.
   - Apply the smallest removal or replacement in the experiment tree, then run the baseline and focused checks and inspect affected callers.
   - Keep the ablation only when required behavior remains, no new failure appears, and production code, dependencies, or design concepts decrease. If the result fails or remains uncertain, reverse only that experiment's hunks.
4. Treat each accepted ablation as the next baseline. Before transferring accepted hunks from a temporary copy, recheck the recorded index and worktree state. Apply them only when they still match and preserve intervening edits; otherwise report the unapplied candidate.
5. Inspect the complete task-owned diff. Reuse passing checks that cover the final content and rerun only when later changes, failures, or unresolved concerns invalidate them. Leave the index and Git history unchanged unless the user asks otherwise.

## Report

Report the pinned scope and keep `Defects`, `Standards`, `Spec`, and `Ponytail` separate. For `Defects`, follow `$review-agent`'s finding format and severity order, use `No findings.` when the pass finds no qualifying defects, and include its overall assessment and material test gaps or residual risks. For each ablation, list its result, evidence, and net reduction. Include final checks and Git state. If no candidate passes, leave the code unchanged.
