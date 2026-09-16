# Skills

Personal agent skills for agents.

## Available Skills

- [`ui-find-icon`](skills/ui-find-icon): Reuse a matching project icon or find one from Remix Icon and Phosphor Icons.
- [`optimize-agents-md`](skills/optimize-agents-md): Audit and optimize AGENTS.md instruction hierarchies with progressive disclosure. Based on <https://www.aihero.dev/a-complete-guide-to-agents-md>.
- [`git-push-lease`](skills/git-push-lease): Safely push a Git branch and use lease protection for forced updates.
- [`squash-commits`](skills/squash-commits): Rebase the current branch onto its integration branch and combine its commits into one.
- [`de-review`](skills/de-review): Review selected changes and remove unnecessary design through ablation experiments.
- [`eli5`](skills/eli5): Explain a topic to a beginner with an HTML artifact, big pictures, and few words.
- [`show-me`](skills/show-me): Explain the current topic with diagrams, code sketches, and HTML artifacts.
- [`unslop`](skills/unslop): Cut AI tells from any writing.

## Installation

List the available skills:

```bash
npx skills add fannheyward/skills --list
```

Install a specific skill globally for Codex:

```bash
npx skills add fannheyward/skills --skill squash-commits --global --agent codex --yes
```

## Maintenance

See the [GPT-6 Astra audit](docs/plan/gpt-6-astra-skills-audit.md) for the optimization rationale and validation scope.
