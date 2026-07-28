---
name: git-push-lease
description: Push Git branches safely, using lease protection for forced updates.
disable-model-invocation: true
---

# Git Push Lease

1. Preserve any remote, refspec, and non-force options supplied by the user. When none are supplied, pass no extra arguments and let Git resolve its configured destination.
2. For a normal update, run `git push` with the preserved arguments.
3. For an explicitly requested forced update, normalize any force syntax and run `git push --force-with-lease` with the preserved arguments.
4. Complete only when the command exits successfully. On failure, report the attempted destination and error, then stop. After a non-fast-forward rejection, require an explicit force request before running step 3.
