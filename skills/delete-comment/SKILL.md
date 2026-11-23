---
name: delete-comment
description: Review code comments, record non-obvious decisions, and prevent new comments from accumulating.
disable-model-invocation: true
argument-hint: "[path or scope]"
---

# Delete comments

Invocation arguments, if any: $ARGUMENTS

Review every code comment in the requested scope. If no scope is given, review the whole codebase. Read the surrounding code before classifying each comment. Preserve tool directives, license notices, and attribution.

| Category | What the comment does | Action |
| --- | --- | --- |
| Tautology | Repeats what is already visible in the code. | Delete it. |
| Excuse | Justifies a workaround that still needs fixing. | File or reuse an issue for the underlying problem, then delete the comment. |
| Stale | Refers to code or implementation details that no longer apply. | Delete it. |
| Decision Record | Explains an important, non-obvious decision. | Move the decision and its rationale into an architecture decision record (ADR), then delete the comment. |

Add or update a lint rule that bans new code comments. If some comments remain, use them as the baseline. Removing one should tighten the baseline. Check that adding a different comment still fails even when the total count stays the same.

Report each comment's original location, category, and outcome, including the issue or ADR where applicable. Estimate how many source lines deleting all comments would save. Count comment-only lines once and report inline removals separately, since they leave the source line in place.
