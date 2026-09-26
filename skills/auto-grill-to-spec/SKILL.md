---
name: auto-grill-to-spec
description: Run grill-with-docs with recommended answers automatically accepted, then turn the completed grill into a local spec. Use for uninterrupted design exploration that produces documents only, without implementation.
---

# Auto Grill to Spec

Run `grill-with-docs` to completion, end the grill, then run `to-spec` on that session and stop. This is a prompt-driven orchestration skill, not a shell command.

## Load the dependencies

Load the installed `grill-with-docs` and its `grilling` and `domain-modeling` dependencies, including the domain document formats they reference. Load `to-spec` when the grill is finished. Use the host's skill mechanism when available; otherwise read their `SKILL.md` files and follow them directly.

Resolve dependencies by name from the current environment's installed skills. If a required dependency is missing, report it and stop without installing anything or inventing its instructions.

## Session overrides

These choices replace the dependencies' interview, confirmation, setup, and publication steps for this workflow:

- Automatically accept the recommended answer to every design question, including terminology, context selection, ADR creation, testing seams, and final shared-understanding confirmation. Do not ask questions in chat or use user-input tools; continue through all rounds without waiting for a reply.
- Explicit user requirements and verified repository facts constrain recommendations. When no recommendation exists, choose the simplest viable answer consistent with those constraints and record the rationale. Mark inferred preferences as automatically selected assumptions, not as statements made or individually approved by the user.
- Look up environmental facts through read-only inspection. An unavailable fact remains an explicitly recorded unknown with a conservative planning assumption; never present an invented fact as evidence. If it prevents a coherent spec, record the blocker in the spec rather than pausing for confirmation.
- Write only the session's local Markdown documents. Do not publish issues, apply remote labels, run setup skills, change agent configuration, commit, or begin implementation, prototypes, tests, dependency installation, or other project changes. Implementation and testing decisions belong in the spec as proposals only.

## 1. Complete the grill and its documents

Use the user's current request and relevant repository context as the topic. Follow `grilling`'s design tree and frontier rounds: formulate every currently answerable question, adopt its recommended answer, then recompute the frontier from those decisions. Resolve dependent questions in later rounds rather than guessing their prerequisites.

Record each round's questions, recommended answers, rationale, and automatically selected assumptions in `.scratch/<topic>/grill.md`. Choose a short topic slug; reuse a session directory only when continuing that same session, otherwise choose a non-conflicting directory.

Follow `domain-modeling` to capture resolved terms in the applicable `CONTEXT.md` and qualifying decisions in `docs/adr/`, using its formats and existing context layout. Create these documents only when there is substantive content; preserve unrelated glossary entries and prior ADRs. Record which documents this session created or updated in the grill record.

The grill ends when the in-scope frontier is empty: every discovered branch has a recorded decision or an explicit evidence blocker with a planning assumption, and the applicable domain documents have been saved. Mark the grill complete with its resulting decisions and remaining unknowns. Treat the upstream final confirmation as automatically satisfied for document synthesis only, then leave the grilling phase.

## 2. Generate the spec and stop

Run `to-spec` using the completed grill, its domain documents, and repository evidence. Follow its spec template, vocabulary, ADR references, testing-seam analysis, and coverage requirements. Automatically accept the recommended testing seams without another interview or confirmation.

Save the result to the same session's `.scratch/<topic>/spec.md`. This local file replaces upstream issue-tracker publication. Missing tracker configuration or triage labels do not require setup and do not block this workflow. Carry forward automatically selected assumptions and unresolved evidence blockers into the spec, and link to the grill record and relevant domain documents.

Verify that the spec reflects the recorded decisions and contains every upstream template section, and that your writes were limited to the session's grill record, applicable domain documents, and spec. Preserve unrelated existing changes.

Finish with links to the produced documents and a brief statement that the grill and spec are complete and implementation has not started. End the workflow here; do not offer or launch an implementation follow-up.
