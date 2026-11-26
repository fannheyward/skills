---
name: f-sharpen
description: "Rewrite a task prompt with primary materials, specific methods, and a way to check the result."
license: MIT
disable-model-invocation: true
---

# f-sharpen

Keep the scope of the original task. Before rewriting the prompt, answer four questions.

1. What would an experienced practitioner do within that scope that the prompt overlooks?
2. Which original records, files, or measurements would they start with?
3. Which methods and tools would they use?
4. What independent evidence would show that the result is right?

Return the rewritten prompt. Have it ask for a prototype and a recommendation based on observations when an experiment can settle a choice. Leave product and preference decisions to the user.

Adapted from [sharpen](https://github.com/cursor/plugins/blob/41e400932eca14f289e7db717a70455256b6d388/pstack/skills/sharpen/SKILL.md).
