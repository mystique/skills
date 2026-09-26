---
name: setup-matt-pocock-local
description: Configure Matt Pocock's engineering skills with AGENTS.md, local Markdown issues, and all default triage labels.
disable-model-invocation: true
---

# Setup Matt Pocock Local

Run `setup-matt-pocock-skills` in the user's target repository with the choices below already supplied. This is a prompt-driven skill, not a shell command.

1. In the user's target repository, check whether it is a Git repository (e.g. `git rev-parse --is-inside-work-tree`). If it is not, run `git init` to initialize it before any other setup step; if `git init` fails, report the error and stop.
2. Load the installed `setup-matt-pocock-skills` skill and its referenced templates. Invoke it through the host's skill mechanism if supported; otherwise read its `SKILL.md` and follow it directly. If it is unavailable, report the missing dependency and stop; do not invent its implementation or silently install it.
3. Apply these explicit choices in place of the upstream defaults and confirmation prompts:
   - **Instruction file:** always use the repository-root `AGENTS.md`, creating it if absent, even when `CLAUDE.md` exists. Leave `CLAUDE.md` unchanged. Update an existing `## Agent skills` block in place and preserve unrelated content.
   - **Issue tracker:** choose **Local markdown**, using `.scratch/<feature>/` and the upstream local template. Do not select GitHub or GitLab based on the remote.
   - **Labels:** accept every upstream default label without renaming or asking for confirmation. The current defaults are `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, and `wontfix`. Retain upstream's condition: write the label mapping and its instruction block only when `triage` is installed. This records vocabulary; it does not create remote labels.
   - These choices are pre-approved: do not pause to confirm them or their resulting draft. For domain layout, retain upstream discovery and defaults; ask only if an unresolved monorepo layout requires a decision.
4. Complete the upstream setup, using its templates rather than duplicating them here. Verify that `AGENTS.md` points to the generated configuration, `docs/agents/issue-tracker.md` specifies local Markdown, and any generated label mapping keeps all upstream defaults. Report the changed files and whether labels were configured or skipped because `triage` is absent.
