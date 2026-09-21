# Rubric: is this a good first issue?

<!--
Built for AI301 Unit 1. Covers the four families from lecture (maintainer
alive, repo in use, newcomer-sized scope, unclaimed) plus the contribution-
policy surface from the evidence guide, because this course's workflow is
AI-assisted.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `not-archived` | The `archived:` flag on the repo line in the repo-facts block. | Reads `archived: no`. An archived repo is read-only, so no pull request can land. | required |
| `recent-default-branch-activity` | The "last 5 default-branch commits" list in repo facts, measured against the capture date stamped on the block. | At least one of the last 5 default-branch commits is dated within 180 days of the capture date. A commit authored solely by a `[bot]` account counts only when its message shows it merged a human pull request (`Merge pull request #N` or an `(#N)` suffix). Quiet default-branch history means a newcomer PR will sit unreviewed. | required |
| `repo-still-shipping` | The "latest release" line and the "last push to any branch" line in repo facts, measured against the capture date. | Either (a) a release dated within 365 days of capture, or (b) a push to any branch within 180 days of capture. Repos with `none published` for releases still pass on the push clause alone — small projects often ship straight from the default branch. | required |
| `scope-is-one-shippable-change` | The issue title, body, labels, and the full comment thread in the bundle. | The issue asks for one bounded change a newcomer could finish in a single PR. Fail when any of these hold: the body or title frames the work as an umbrella / meta / tracking / mega-issue or as a checklist of separately shippable items; the ask is codebase-wide or targets core internals as the whole task; the thread shows an unsettled design debate with no maintainer decision; the post is a usage/support question rather than a change request; or the body is a one-line feature wish with no specification and the product decision is still open. A terse body, missing reproduction steps, or a thin acceptance checklist does **not** fail by itself — grade the size of the work, not the polish of the write-up. | required |
| `not-actively-claimed` | The `this issue: assignees:` and `linked PRs:` lines in repo facts, plus claim-style comments in the thread ("I'll take this", "working on this", "can I work on this") with their dates, measured against the capture date. | All three hold: (1) assignees is `none` / empty; (2) no linked PR is in the `open` state; (3) no unanswered claim comment dated within 120 days of capture. A claim older than 120 days with no open linked PR is stale and does not block. A closed or merged linked PR is not an active claim. | required |
| `ai-contribution-allowed` | The "contribution policy" line in repo facts (including any Generative AI / AI use section quoted there, and any AI_POLICY / AGENTS.md note). | The policy does not ban AI-generated or AI-assisted contributions outright. An explicit ban fails. Disclosure, "understand and test what you submit", and human-review requirements **pass** — those are terms to follow, not walls. Silence passes: most repos state nothing, and nothing is not a restriction. "Strongly discourage" language that still allows human-reviewed AI assistance also passes. | required |
| `newcomer-signposted` | The issue's labels, and the `author_association` of the opener. | Carries a newcomer-facing label (`good first issue`, `good-first-issue`, `help wanted`, `beginner`, `easy`, or `Easy to Fix`) **or** was opened by an `OWNER`, `MEMBER`, or `COLLABORATOR`. Ranking only. | preferred |

## Verdict rule

`accept` only if every `required` check is `pass`. Any required `fail` yields `reject`.

`unclear` on a required check counts as `fail`. In eval mode the bundle is the whole world, so missing evidence is a real answer — not a gap to invent around. A first issue I cannot verify is not one I should take.

`preferred` checks never change the verdict. Among issues that already `accept`, prefer ones that are newcomer-signposted when ranking.
