# Agent Skills

A collection of reusable agent skills for common software development workflows.

## Available Skills

| Skill | Description |
| --- | --- |
| [`git-commit`](skills/git-commit/SKILL.md) | Review, split, and create verifiable Git commits. Distinguishes message-only, preview, and execute; preserves staging boundaries; prefers a Conventional Commits message with a body. |
| [`ui-variants`](skills/ui-variants/SKILL.md) | Explicit-only: build genuinely different versions of one UI piece behind a visual picker, then promote the chosen variant. |

## Installation

Install all available skills:

```bash
npx skills@latest add mystique/skills
```

Install a specific skill:

```bash
npx skills@latest add mystique/skills --skill git-commit
npx skills@latest add mystique/skills --skill ui-variants
```
