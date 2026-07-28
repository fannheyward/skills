# Skills

Personal agent skills for agents.

## Available Skills

- [`git-push-lease`](skills/git-push-lease): Safely push a Git branch and use lease protection for forced updates.
- [`squash-commits`](skills/squash-commits): Rebase the current branch onto its integration branch and combine its commits into one.

## Installation

List the available skills:

```bash
npx skills add fannheyward/skills --list
```

Install a specific skill globally for Codex:

```bash
npx skills add fannheyward/skills --skill squash-commits --global --agent codex --yes
```
