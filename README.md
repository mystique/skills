# Agent Skills

Reusable agent skills for Git workflows, product UI design, UI exploration, and spec writing. Each skill is a folder under `skills/` with a `SKILL.md` that agents load on demand.

## Available Skills

| Skill | Model invocation | Description |
| --- | --- | --- |
| [`git-commit`](skills/git-commit/SKILL.md) | Implicit allowed | Create, preview, or split Git commits. Follows repository conventions, preserves existing staging, verifies each commit, and never adds agent attribution. |
| [`interface-design`](skills/interface-design/SKILL.md) | Implicit allowed | Craft-first design for product UI: dashboards, admin panels, SaaS apps, tools, and data interfaces. Not for marketing pages or landing pages. |
| [`ui-variants`](skills/ui-variants/SKILL.md) | Explicit only | Build genuinely different versions of one UI piece behind a visual picker, then promote the chosen one and remove the prototype. |
| [`setup-matt-pocock-local`](skills/setup-matt-pocock-local/SKILL.md) | Explicit only | Configure Matt Pocock's engineering skills with a root `AGENTS.md`, local Markdown issues, and default triage labels. |
| [`auto-grill-to-spec`](skills/auto-grill-to-spec/SKILL.md) | Implicit allowed | Run `grill-with-docs` with recommended answers auto-accepted, then write a local spec. Produces documents only; no implementation. |

## Installation

Install all skills:

```bash
npx skills@latest add mystique/skills
```

Install a specific skill:

```bash
npx skills@latest add mystique/skills --skill git-commit
npx skills@latest add mystique/skills --skill interface-design
npx skills@latest add mystique/skills --skill ui-variants
npx skills@latest add mystique/skills --skill setup-matt-pocock-local
npx skills@latest add mystique/skills --skill auto-grill-to-spec
```

`setup-matt-pocock-local` and `auto-grill-to-spec` depend on skills from other repositories; see their sections below.

## Usage

### git-commit

| Invocation | Behavior |
| --- | --- |
| `/git-commit` (or a natural-language request) | Create the requested commit(s) |
| `/git-commit --preview` | Show the proposed groups and messages; change nothing |
| `/git-commit --message-only` | Return only the commit message; change nothing |

Message format follows the repository's conventions first. Conventional Commits 1.0.0 with a body is the fallback. The skill never bypasses hooks, amends, or force-pushes unless you explicitly ask.

### interface-design

Reads `.interface-design/system.md` when present and applies its decisions. Uses an inline render tool or an image-generation tool when the session provides one; otherwise it works from code, tokens, and written proposals.

### ui-variants

Explicit invocation only. Production code is untouched until you promote a variant.

| Invocation | Behavior |
| --- | --- |
| `<description>` | Build 3 variants (use `<description> x5` for up to 5) behind the picker |
| `riff <variant>` | New round that diverges around the named variant |
| `keep <variant>` | Promote the variant into the codebase and delete the prototype |
| `keep <variant>, leave the picker` | Promote and keep the prototype surface |

The picker is a fixed bottom-center pill specified in [`PICKER.md`](skills/ui-variants/PICKER.md). Keys: `1`–`N` or `←`/`→` switch variants, `R` replays the animation. The selected variant is stored in the `?v=` URL parameter.

### setup-matt-pocock-local

Requires the upstream `setup-matt-pocock-skills` skill, which this repository does not bundle:

```bash
npx skills@latest add mattpocock/skills --skill setup-matt-pocock-skills
```

Run `/setup-matt-pocock-local` (or `$setup-matt-pocock-local` in Codex) in the target repository. It runs the upstream setup with these choices pre-approved:

- Instructions go in the repository-root `AGENTS.md`; `CLAUDE.md` is left unchanged.
- Issues are local Markdown under `.scratch/<feature>/`.
- Default triage labels are accepted. Label mapping is written only when `triage` is installed. Nothing is created on the remote.

If the directory is not a Git repository, the skill runs `git init` first.

### auto-grill-to-spec

Requires these skills to be installed in the environment: `grill-with-docs`, `grilling`, `domain-modeling`, and `to-spec`. It does not install them; if one is missing, it reports the gap and stops.

Output, all under `.scratch/<topic>/`:

- `grill.md`: each round's questions, recommended answers, and automatic assumptions
- `spec.md`: the generated spec, with unresolved evidence blockers recorded
- `CONTEXT.md` and `docs/adr/`: updated only when the session produces substantive terms or decisions

The skill makes no commits, publishes no issues, and starts no implementation.

## Repository Layout

```text
skills/
└── <skill-name>/
    ├── SKILL.md            # frontmatter (name, description) and instructions
    ├── agents/openai.yaml  # UI metadata and invocation policy for OpenAI/Codex
    └── ...                 # optional supporting files, e.g. ui-variants/PICKER.md
```

Each `SKILL.md` frontmatter `name` matches its folder. When you add or rename a skill, update the tables in this README.

## Contributing

Commits follow Conventional Commits with the skill as scope, for example `feat(git-commit): ...` or `feat: add auto grill to spec skill`.
