---
name: optimize-agents-md
description: Audit and optimize AGENTS.md instruction hierarchies with progressive disclosure.
disable-model-invocation: true
---

# Optimize AGENTS.md

Build a small, current instruction hierarchy that gives agents universal context up front and routes conditional guidance only when it applies.

## Establish the Boundary

1. Find the `AGENTS.md` files that govern the target and read them from the outermost scope to the closest scope. Apply the runtime's precedence rules; among repository policies, closer instructions override broader ones.
2. Inspect current repository configuration, documentation, and conventions before stating project facts or commands. Preserve unrelated worktree changes.
3. Match the work to the user's authorization:
   - When asked only to **review**, **audit**, **assess**, or **plan**, remain read-only and return findings plus a proposed hierarchy.
   - When asked to **create**, **refactor**, **simplify**, **split**, **fix**, or **optimize**, apply the changes after resolving material conflicts.

## Audit the Instructions

Inventory the applicable instructions and classify each one by the narrowest scope where it remains useful:

- **Universal**: needed for every task in the current scope.
- **Conditional**: needed only for a domain or activity such as testing, TypeScript, API design, releases, or Git work.
- **Local**: needed only within a package or subtree.
- **Deletion candidate**: duplicated, obsolete, contradicted by the repository, too vague to act on, or a no-op the agent already follows by default.
- **Conflict**: incompatible instructions that could change behavior depending on which one wins.

Verify each factual instruction against the repository. Configuration, scripts, and the current tree are the source of truth; document a discoverable fact only when repeating it prevents a likely mistake or explains a non-obvious constraint.

For every material conflict, identify the competing instructions, their locations, and the behavioral consequence. Batch the conflicts when practical, ask the user which version to keep, and wait before rewriting the affected policy. Continue only with unaffected work while the choice is unresolved.

## Design Progressive Disclosure

Treat the root as an **instruction budget**: every line loads for every task in its scope, so each line must earn universal relevance.

Place each retained instruction according to its actual reach:

| Reach | Location |
| --- | --- |
| Every task in the current scope | That scope's `AGENTS.md` |
| One domain or activity | A focused linked document with an explicit trigger in the pointer |
| One package or subtree | A nested `AGENTS.md`, accounting for the ancestor instructions it inherits |
| A reusable multi-step procedure | A skill, when the target agent system supports skills |
| A fact that is cheap to discover | Its existing configuration or source file, not a copied documentation cache |

Use this as a root-file pruning heuristic, not a rigid schema:

- a one-sentence project purpose;
- a non-default package manager;
- non-standard build or typecheck commands;
- safety, precedence, collaboration, or other rules genuinely relevant to every task in that scope.

Keep branch-specific details behind links whose wording states when to read them. Create only links and files that serve a real branch. Co-locate each concept's rules and caveats, and keep one authoritative copy of each instruction.

Prefer stable capabilities, domain language, and decision constraints over directory tours or brittle file maps. Keep exact paths and commands when they are operational invariants; verify them before retaining them.

## Write the Hierarchy

- Preserve the user's policy choices and the repository's established language and terminology. Do not invent conventions to make the file look complete.
- Express instructions positively, directly, and with a checkable outcome. Explain non-obvious reasons when they change how the agent should decide.
- Keep the root focused on universal guidance. Move conditional details to the smallest useful set of linked documents, and use nested `AGENTS.md` files only when subtree scope is real.
- Update pointers when files move, and use valid relative Markdown links so the hierarchy remains navigable.
- When creating a policy from scratch, derive it from verified repository needs instead of generating a generic project inventory.

In read-only mode, present the proposed root contents, document or nested-policy tree, relocation map, deletion candidates with reasons, and unresolved conflicts without editing files.

## Verify

Read the resulting hierarchy as the agent will receive it and require all of these conditions:

- every root instruction applies throughout its scope;
- every conditional instruction is reachable through a pointer that names its trigger;
- every new or changed link resolves;
- inherited root and nested policies do not conflict or duplicate one another;
- retained facts and commands match the current repository;
- the complete diff contains only authorized policy changes and passes the repository's text checks, including `git diff --check` when Git is available.

Report what stayed at the root, what moved and why, what was deleted and why, how conflicts were resolved, and which verification checks passed.
