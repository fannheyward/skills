---
name: f-deslop
description: "Clean up redundant AI-generated code in a branch diff using the surrounding code as the style guide."
license: MIT
---

# f-deslop

Review the branch diff against the requested base or the repository's integration branch. Limit edits to issues introduced by that diff. Compare each candidate with nearby code.

- Remove comments that repeat the code or conflict with local conventions.
- Remove redundant checks and exception handlers only where the caller or type already guarantees the condition.
- Replace casts to `any` that bypass a type error with the correct type or narrowing.
- Flatten nesting with an early return when it makes the path easier to follow.

Keep edits small. Preserve observable behavior unless the change fixes a clear bug. Summarize the cleanup in one to three sentences.

Adapted from [deslop](https://github.com/cursor/plugins/blob/41e400932eca14f289e7db717a70455256b6d388/cursor-team-kit/skills/deslop/SKILL.md).
