# Optimize AGENTS.md Skill Plan

## Problem

Create a reusable skill that applies the progressive-disclosure guidance and refactoring prompt from [A Complete Guide To AGENTS.md](https://www.aihero.dev/a-complete-guide-to-agents-md) without copying the article into every invocation. The skill should improve existing `AGENTS.md` hierarchies and support new ones while preserving repository facts, user intent, and local precedence.

## Design Decisions

- Name the skill `optimize-agents-md`. The action-oriented name matches its primary outcome and is easier to recall for explicit invocation than a generic domain-only name.
- Make the skill explicit-only because the user wants it loaded only after typing `$optimize-agents-md`. Enforce this in both skill frontmatter and UI policy.
- Keep the workflow in one `SKILL.md`; the task has one coherent path and does not justify extra reference files or scripts.
- Treat contradictions as a decision gate. Report each material conflict and obtain the user's choice before rewriting the affected policy.
- Treat the article's minimal root contents as a pruning heuristic, not an absolute schema. Universally applicable safety, precedence, or collaboration rules may also belong at the root.
- Separate read-only review from authorized edits. A review produces findings and a proposed hierarchy; a create, refactor, fix, or optimize request applies the changes.
- Prefer stable capabilities and domain concepts over copied directory maps, while retaining exact paths or commands when they are genuine operational invariants.

## Implementation Steps

- [x] Rename the skill directory to `skills/optimize-agents-md`.
- [x] Update skill frontmatter and UI metadata for the new name and explicit-only invocation.
- [x] Update the repository catalog and plan references.
- [x] Verify that discovery exposes only the new name and that both invocation controls disable implicit use.
- [x] Inspect the complete diff and confirm every change belongs to this skill.

## Risks and Mitigations

- Over-pruning important policy: classify instructions by actual scope and preserve universal constraints even when they exceed the article's minimal examples.
- Hiding required guidance behind weak links: make every pointer state the condition that triggers reading its target.
- Creating stale documentation: verify claims against current repository configuration and avoid duplicating facts that are cheap to discover.
- Changing policy while conflicts remain unresolved: pause only the affected edit and request a user decision.
- Expanding review into mutation: map review verbs to read-only output and mutation verbs to edits.

## Success Criteria

- The skill is available as `$optimize-agents-md` and cannot be selected implicitly.
- Its workflow covers contradiction handling, root essentials, conditional grouping, nested monorepo scope, deletion candidates, implementation boundaries, and verification.
- Root instructions stay limited to guidance needed across the root's full scope; conditional guidance is reachable through explicit trigger links.
- `SKILL.md`, `agents/openai.yaml`, and `README.md` are consistent and pass metadata and discovery checks.

## Progress

- Source article, closing prompt, repository conventions, and authoring guidance reviewed.
- Initial skill implementation passed validation and repository discovery.
- Rename and explicit-only conversion complete.
- YAML assertions confirmed the new name, default prompt, and both explicit-only controls; repository discovery exposes only `optimize-agents-md`.
- The bundled validator rejects the supported `disable-model-invocation` field because its schema is stale. Independent YAML parsing, discovery, placeholder, whitespace, and diff checks cover this known incompatibility.

## Related Files

- `skills/optimize-agents-md/SKILL.md`
- `skills/optimize-agents-md/agents/openai.yaml`
- `README.md`
