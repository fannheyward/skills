# Skills

Personal agent skills for agents.

## Available Skills

- [`ui-find-icon`](skills/ui-find-icon): Find and use a UI icon from Remix Icon or Phosphor Icons.
- [`optimize-agents-md`](skills/optimize-agents-md): Audit and optimize AGENTS.md instruction hierarchies with progressive disclosure. Based on <https://www.aihero.dev/a-complete-guide-to-agents-md>.
- [`git-push-lease`](skills/git-push-lease): Safely push a Git branch and use lease protection for forced updates.
- [`squash-commits`](skills/squash-commits): Rebase the current branch onto its integration branch and combine its commits into one.
- [`de-review`](skills/de-review): Review selected changes and remove unnecessary design through ablation experiments.

## Installation

List the available skills:

```bash
npx skills add fannheyward/skills --list
```

Install a specific skill globally for Codex:

```bash
npx skills add fannheyward/skills --skill squash-commits --global --agent codex --yes
```
