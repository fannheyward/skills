---
name: git-push-lease
description: Push Git branches safely, using lease protection for forced updates.
disable-model-invocation: true
---

# Git Push Lease

1. Preserve any remote, refspec, and non-force options supplied by the user. When none are supplied, pass no extra arguments and let Git resolve its configured destination.
2. For a normal update, run `git push` with the preserved arguments.
3. For a forced update requested in this conversation, normalize force syntax to `git push --force-with-lease` with the preserved arguments. Retain any user-supplied lease ref and expected OID. Existing authorization for the same destination and update remains valid.
4. A zero exit status completes the requested push, or only its preview when `--dry-run` is present. Report that distinction and the destination shown by Git. On failure, report the error and stop. A non-fast-forward rejection does not authorize a forced update; step 3 requires the user's force request.
