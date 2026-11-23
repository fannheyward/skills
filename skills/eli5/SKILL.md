---
name: eli5
description: Explain a topic like I'm a 5 year old.
disable-model-invocation: true
argument-hint: "[topic]"
---

# eli5

Explain like I'm someone who knows nothing about this topic, using a HTML artifact with big pictures and few words.

Topic: $ARGUMENTS

When no topic is supplied, use the current topic of conversation.

Adapted from [eli5](https://github.com/anthropics/claude-plugins-community/blob/main/eli5/skills/eli5/SKILL.md). This version supports both Claude Code and Codex invocation.
