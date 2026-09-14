---
name: ui-find-icon
description: Find and use a UI icon from Remix Icon or Phosphor Icons.
disable-model-invocation: true
---

# Find UI Icon

Find an interface icon that fits the requested meaning and existing UI. Recommend it for a lookup or integrate it when the user requests a code change.

## Establish the target

1. Identify the icon's meaning, state, target platform, and expected size. When working in a repository, inspect nearby UI code and existing icon dependencies before searching.
2. Infer platform and style from adjacent code when the choice is low risk. Ask only when missing information would change the icon's meaning or implementation.
3. If an existing project icon meets the request, verify its identifier and variant in the installed package or assets, follow nearby usage, and proceed to delivery. Search the websites when a new icon is needed or the user requests alternatives or a library comparison.

## Search and choose

1. Use `ego-browser` to search [Remix Icon](https://remixicon.com/) first, then [Phosphor Icons](https://phosphoricons.com/). Use English search terms and relevant synonyms because the two libraries may use different vocabulary, such as `microphone` and `mic`. Search both sites unless the user limits the request to one library.
2. Open each promising result and verify its exact displayed identifier and variant. For Phosphor, record the selected Thin, Light, Regular, Bold, Fill, or Duotone weight. For Remix, record the full identifier, including its `-line` or `-fill` suffix.
3. Keep the strongest candidate from each library you search. Judge semantic accuracy, clarity at the target size, state pairing, and consistency with adjacent icons.
4. Prefer a Remix icon when it is a good semantic and visual match. Choose Phosphor when the project already uses it, Remix has no suitable result, or the interface requires multiple weights or Duotone.
5. Recommend one final icon. Never invent an identifier. If neither library has a good match, state that clearly and return the nearest alternatives instead.

## Deliver or apply

- For a lookup, report one recommendation, its exact identifier and variant, the library, a verified official URL or local source path, and a brief reason. Include at most one alternative from the other searched library unless the user asks for more.
- For a code change, follow the installed package's current API and existing usage in nearby code. Use the project's existing vector-asset pipeline when no library package is installed. Add or replace a dependency only when the user explicitly requests it.
- Preserve platform behavior: give meaningful controls an accessible label, hide decorative icons from accessibility, and mirror directional icons when the existing UI supports right-to-left layouts.
- For code changes, verify that the identifier exists, its use matches the installed API, accessibility remains correct, and the complete diff stays in scope. Use a focused build, typecheck, test, or visual check when those checks resolve a remaining risk. Reuse results for unchanged final content; report any relevant check that could not run.
