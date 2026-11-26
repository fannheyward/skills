# Skills

Personal agent skills for agents.

## Available Skills

- [`f-ui-find-icon`](skills/f-ui-find-icon): Reuse a matching project icon or find one from Remix Icon and Phosphor Icons.
- [`f-optimize-agents-md`](skills/f-optimize-agents-md): Audit and optimize AGENTS.md instruction hierarchies with progressive disclosure. Based on <https://www.aihero.dev/a-complete-guide-to-agents-md>.
- [`f-git-push-lease`](skills/f-git-push-lease): Safely push a Git branch and use lease protection for forced updates.
- [`f-squash-commits`](skills/f-squash-commits): Rebase the current branch onto its integration branch and combine its commits into one.
- [`f-review`](skills/f-review): Review selected changes for standards, spec, complexity, and module design, then remove unnecessary abstractions through ablation experiments.
- [`f-eli5`](skills/f-eli5): Explain a topic to a beginner with an HTML artifact, big pictures, and few words.
- [`f-show-me`](skills/f-show-me): Explain the current topic with diagrams, code sketches, and HTML artifacts.
- [`f-unslop`](skills/f-unslop): Cut AI tells from any writing.
- [`f-delete-comment`](skills/f-delete-comment): Classify code comments, move decisions into ADRs, and track workarounds in issues.
- [`f-sharpen`](skills/f-sharpen): Rewrite a task prompt with primary materials, specific methods, and a way to check the result.
- [`f-reframe`](skills/f-reframe): Explain the domain terms behind a project and use them to rewrite the user's description.
- [`f-deslop`](skills/f-deslop): Clean up redundant AI-generated code in a branch diff using the surrounding code as the style guide.

## Installation

List the available skills:

```bash
npx skills add fannheyward/skills --list
```

Install a specific skill globally for Codex:

```bash
npx skills add fannheyward/skills --skill f-squash-commits --global --agent codex --yes
```

Install a specific skill globally for Claude Code:

```bash
npx skills add fannheyward/skills --skill f-squash-commits --global --agent claude-code --yes
```
