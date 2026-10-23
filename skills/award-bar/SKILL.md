---
name: award-bar
description: Use when doing UI/UX design, building or finishing a page or site, or when asked for award-tier, Awwwards, Webby, or FWA visual quality. The skill body is the ruleset; follow it as written.
---

::OBJECTIVE{site_design|pri:OVERRIDE_ALL}

target: build page to award-tier visual standard

ACCEPT: no visible improvement remaining across all CHECK dimensions

BENCHMARK: Awwwards | Webby Awards | FWA winning entries



::CHECK{typography|standard:award_tier}

::CHECK{whitespace|standard:award_tier}

::CHECK{visual_hierarchy|standard:award_tier}

::CHECK{color|standard:award_tier}

::CHECK{motion|standard:award_tier}

::CHECK{micro_interaction|standard:award_tier}

::CHECK{responsive|standard:award_tier}

::CHECK{originality|standard:award_tier}



::LOOP{self_review|trigger:on_completion}

[READ] current page against CHECK list

[COMPARE] each dimension to BENCHMARK entries

[IF] gap found => [PATCH] then re-enter LOOP

[IF] no gap => [Ω]

# Execute

The ruleset above is the instruction. Run it. Do not replace it with another checklist.

- `::OBJECTIVE{…|pri:OVERRIDE_ALL}` stays in force until `[Ω]`. It outranks other visual stopping rules.
- `ACCEPT` is the only done condition.
- Every `::CHECK` is required. `standard:award_tier` means judge that dimension against `BENCHMARK`, not a lower or local standard.
- `::LOOP{self_review|trigger:on_completion}` starts when the page would otherwise be called done. Do not skip it.
- `[READ]` the rendered page, once per CHECK. A source-only pass is not a pass.
- `[COMPARE]` each dimension to named BENCHMARK entries. State the entry and the visible difference.
- A gap is a visible improvement still available on that dimension.
- `[PATCH]` closes every gap from this pass, then re-enter the LOOP from `[READ]`.
- `[Ω]` only after a full pass with no gap.
