---
name: ui-find-icon
description: Find and use an UI icon from Remix Icon or Phosphor Icons.
disable-model-invocation: true
---

# Find UI Icon

Find the best-matching interface icon on the official Remix Icon and Phosphor Icons websites, then recommend it or add it to the target project.

## Establish the target

1. Identify the icon's meaning, state, target platform, and expected size. When working in a repository, inspect nearby UI code and existing icon dependencies before searching.
2. When the project's current icon library includes a good match, use that icon and follow the existing visual style. Infer the platform and style from adjacent code when doing so is low risk; ask only when missing information would materially change the result.

## Search and choose

1. Use `ego-browser` to search [Remix Icon](https://remixicon.com/) first, then [Phosphor Icons](https://phosphoricons.com/). Use English search terms and relevant synonyms because the two libraries may use different vocabulary, such as `microphone` and `mic`. Search both sites unless the user limits the request to one library.
2. Open each promising result and verify its exact displayed identifier and variant. For Phosphor, record the selected Thin, Light, Regular, Bold, Fill, or Duotone weight. For Remix, record the full identifier, including its `-line` or `-fill` suffix.
3. Keep the strongest candidate from each library you search. Judge semantic accuracy, clarity at the target size, state pairing, and consistency with adjacent icons.
4. Prefer a Remix icon when it is a good semantic and visual match. Choose Phosphor when the project already uses it, Remix has no suitable result, or the interface requires multiple weights or Duotone.
5. Recommend one final icon. Never invent an identifier. If neither library has a good match, state that clearly and return the nearest alternatives instead.

## Deliver or apply

- For a lookup, report the recommendation, its exact identifier and variant, the library, the official source URL, and a brief reason for choosing it. Include at most one alternative from the other searched library unless the user asks for more.
- For a code change, follow the installed package's current API and existing usage in nearby code. Use the project's existing vector-asset pipeline when no library package is installed. Add or replace a dependency only when the user explicitly requests it.
- Preserve platform behavior: give meaningful controls an accessible label, hide decorative icons from accessibility, and mirror directional icons when the existing UI supports right-to-left layouts.
- If you change code, run the smallest relevant build, typecheck, or test and inspect the complete diff. Finish only when the implemented identifier exists in the selected library and every change belongs to the request.
