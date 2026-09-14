---
name: optimize-agents-md
description: Audit and optimize AGENTS.md instruction hierarchies with progressive disclosure.
disable-model-invocation: true
---

# Optimize AGENTS.md

Build a small, current instruction hierarchy that gives agents universal context up front and routes conditional guidance only when it applies.

## Establish the boundary

1. Find the `AGENTS.md` files that govern the target and read them from the outermost scope to the closest scope. Apply the runtime's precedence rules; among repository policies, closer instructions override broader ones.
2. Inspect current repository configuration, documentation, and conventions before stating project facts or commands. Preserve unrelated worktree changes.
3. Read the complete request and prior authorization to select the mode. A review, audit, assessment, or plan alone is read-only. A request to create, refactor, simplify, split, fix, or optimize authorizes the scoped edits, including when paired with an audit. Honor an explicit request for plan confirmation before editing.

## Audit the instructions

Inventory the applicable instructions and classify each one by the narrowest scope where it remains useful:

- **Universal**: needed for every task in the current scope.
- **Conditional**: needed only for a domain or activity such as testing, TypeScript, API design, releases, or Git work.
- **Local**: needed only within a package or subtree.
- **Deletion candidate**: duplicated, obsolete, contradicted by the repository, too vague to act on, or a no-op the agent already follows by default.
- **Conflict**: incompatible instructions that could change behavior depending on which one wins.

Verify each factual instruction against the repository. Configuration, scripts, and the current tree are the source of truth; document a discoverable fact only when repeating it prevents a likely mistake or explains a non-obvious constraint.

Resolve conflicts through the runtime's instruction hierarchy, the user's explicit choices, and repository precedence. Record which source governs each material conflict. Ask only when an unresolved choice would change policy, scope, or correctness. Present the competing rules, locations, consequence, and proposed resolution; pause the affected edit and continue independent authorized work.

## Design progressive disclosure

Treat the root as an **instruction budget**: every line loads for every task in its scope, so each line must earn universal relevance.

Place each retained instruction according to its actual reach:

| Reach | Location |
| --- | --- |
| Every task in the current scope | That scope's `AGENTS.md` |
| One domain or activity | A focused linked document with an explicit trigger in the pointer |
| One package or subtree | A nested `AGENTS.md`, accounting for the ancestor instructions it inherits |
| A reusable multi-step procedure | A skill, when the target agent system supports skills |
| A fact that is cheap to discover | Its existing configuration or source file, not a copied documentation cache |

Keep branch-specific details behind links whose wording states when to read them. Create a linked file only when a substantial conditional branch benefits from separate loading; keep a short, coherent policy in one file. Co-locate each concept's rules and caveats, and keep one authoritative copy of each instruction.

Prefer stable capabilities, domain language, and decision constraints over directory tours or brittle file maps. Keep exact paths and commands when they are operational invariants; verify them before retaining them.

## Write the hierarchy

- Preserve the user's policy choices and the repository's established language and terminology. Do not invent conventions to make the file look complete.
- Express instructions positively, directly, and with a checkable outcome. Explain non-obvious reasons when they change how the agent should decide.
- Keep the root focused on universal guidance. Move conditional details to the smallest useful set of linked documents, and use nested `AGENTS.md` files only when subtree scope is real.
- Update pointers when files move, and use valid relative Markdown links so the hierarchy remains navigable.
- When creating a policy from scratch, derive it from verified repository needs instead of generating a generic project inventory.

In read-only mode, report actionable findings with source locations and a proposed change. Include draft contents or a relocation map when a hierarchy change needs them.

## Verify

Read the resulting hierarchy as the agent will receive it and require all of these conditions:

- every root instruction applies throughout its scope;
- every conditional instruction is reachable through a pointer that names its trigger;
- every new or changed link resolves;
- inherited root and nested policies do not conflict or duplicate one another;
- retained facts and commands match the current repository;
- the complete diff contains only authorized policy changes and passes the repository's text checks, including `git diff --check` when Git is available.

Reuse checks that passed against the final content. Expand verification only for new changes, failures, or unresolved concerns. Report the resulting hierarchy, material changes and reasons, conflict resolutions, and verification limits. Omit empty report sections.
