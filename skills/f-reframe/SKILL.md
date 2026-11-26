---
name: f-reframe
description: "Explain the domain terms behind a project and use them to rewrite the user's description."
license: MIT
disable-model-invocation: true
---

# f-reframe

Start with the user's own description, files, and code. If several problems fit, name the two or three plausible interpretations and the observation that distinguishes each. Explain which best fits the evidence.

1. Identify 8 to 12 terms, ranked by how much each changes what gets built. For each, give a plain definition, identify the part of the user's description it names, link to a project, paper, or system that uses it that way, and show what the term lets the user ask for.
2. Compare two or three neighboring fields that have solved a similar problem. Explain which ideas carry over and where the comparison breaks down.
3. Identify an omission that would matter to the project.
4. Rewrite the user's description with the terms that fit.

Open each cited source and check its use of the term. Omit entries you cannot substantiate, even if that leaves fewer terms.

Adapted from [reframe](https://github.com/cursor/plugins/blob/41e400932eca14f289e7db717a70455256b6d388/pstack/skills/reframe/SKILL.md).
