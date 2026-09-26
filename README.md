# Agent Skills

A collection of reusable agent skills for common software development workflows.

## Available Skills

| Skill | Description |
| --- | --- |
| [`git-commit`](skills/git-commit/SKILL.md) | Review, split, and create verifiable Git commits. Distinguishes message-only, preview, and execute; preserves staging boundaries; prefers a Conventional Commits message with a body. |
| [`interface-design`](skills/interface-design/SKILL.md) | Craft-first product interface design for dashboards, admin panels, SaaS apps, tools, and data interfaces. Focuses on visual hierarchy, intentional token systems, interactive states, and production polish. |
| [`ui-variants`](skills/ui-variants/SKILL.md) | Explicit-only: build genuinely different versions of one UI piece behind a visual picker, then promote the chosen variant. |
| [`setup-matt-pocock-local`](skills/setup-matt-pocock-local/SKILL.md) | Explicit-only: configure Matt Pocock skills with `AGENTS.md`, local issues, and all default triage labels. |

## Installation

Install all available skills:

```bash
npx skills@latest add mystique/skills
```

Install a specific skill:

```bash
npx skills@latest add mystique/skills --skill git-commit
npx skills@latest add mystique/skills --skill interface-design
npx skills@latest add mystique/skills --skill ui-variants
```

## Setup Matt Pocock Local

`setup-matt-pocock-local` calls the upstream `setup-matt-pocock-skills` with pre-approved choices: repository-root `AGENTS.md`, local Markdown issues under `.scratch/<feature>/`, and every default triage label. It leaves `CLAUDE.md` unchanged. As upstream specifies, labels are configured only when `triage` is installed.

Install the upstream dependency and this skill:

```bash
npx skills@latest add mattpocock/skills --skill setup-matt-pocock-skills
npx skills@latest add mystique/skills --skill setup-matt-pocock-local
```

Invoke `/setup-matt-pocock-local` (or `$setup-matt-pocock-local` in Codex) in the target repository.
