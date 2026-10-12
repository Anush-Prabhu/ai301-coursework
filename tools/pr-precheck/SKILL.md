---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: **is this
ready to submit?** A PR package is a candidate pull request (title,
description, commits, diff, test evidence), read against the plan it
claims to implement and the issue that plan belongs to. You do not
answer from gut feel, and this file no longer invents a workflow: you
answer by executing the student-authored grading procedure in
`procedure.md`, which applies the rubric in `rubric.md` to evidence
gathered per `references/evidence-guide.md`.

## The question

Grade exactly one package per run. Decide only whether that package is
ready to submit (`accept`) or must be held (`reject`). Do not grade a
different question, do not score style for its own sake, and do not
invent checks outside `rubric.md`.

## Inputs and modes

One of:

- **Live mode**: the student's own submission before it goes out.
  Inputs: their `plan.md` (including any `## Deviations` notes), the
  branch diff produced by `git diff main...HEAD` (three dots) from the
  working copy, their draft PR title and description (usually
  `pr_draft.md`), and their test evidence (usually `test_evidence.md`),
  read against their issue. Gather issue-side evidence live (thread,
  PR template, stated policy) per `references/evidence-guide.md`. A
  house-chain student reads the house plan and house repro pack
  instead of a personal posted plan; the same checks still apply.
- **Eval mode**: a package bundle (markdown containing repo facts,
  issue/thread, plan context, and the candidate PR with title,
  description, commits, diff, and test evidence). Use ONLY the bundle
  text as evidence. Do not fetch anything; the bundle is the whole
  world. Eval mode always grades a complete package: every check,
  full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. It names where the student's PR must live and the house rules
that apply there; a house rule changes how evidence is read in that
environment. Refuse to grade a package for a PR outside the scoped
source. If the scope's `Repo:` line still carries an unfilled
placeholder, stop without grading and tell the student to fill
`scope.md` with their section's Path Review repo; never guess a scope.
In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream. Hold the outgoing PR **title and description**
against those rules and report any broken rule in the summary, quoting
the rule. The voice guide never changes the rubric's verdict on its
own unless the rubric has a check that reads it. In eval mode, ignore
`voice-guide.md` entirely: voice is personal and carries no gold
labels; universal communication-quality checks live in the rubric.

## Component reads

Read `rubric.md`. It defines the checks table and the verdict rule.
`references/evidence-guide.md` maps where each evidence family lives
in a PR package (and, live, on disk / GitHub). **Execute
`procedure.md` as written** for read order, evidence gathering, check
execution, and verdict assembly. Where the procedure is silent, note
the gap in your summary rather than silently inventing a step. If
`rubric.md` has no checks filled in, or `procedure.md` has no steps
filled in, stop and say so: this skill cannot grade without a rubric
AND a procedure, and that is by design.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict. Emit a fenced JSON block, then
nothing else after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Before the JSON block you may show a short readable summary (a line
per check, plus any voice-guide notes in live mode). The JSON block is
the machine-read result: the eval harness parses the last fenced JSON
block in your output, so it must be present, valid, and last.

## Grading discipline

- Evidence first: never grade a check without naming the fact that
  decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready
  and a beautiful confident one can hide drift or debris. Every check
  reads the artifact itself against the plan, the issue, and the
  stated standards, never the formatting.
- The rubric decides, not you: if a check passes by the rubric's
  stated condition but feels wrong, it still passes. Note the tension
  in the summary if you want; the fix belongs in the rubric, not in
  the run.
- The procedure decides how, not you: follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. If the rule
  does not say, treat `unclear` as `fail`: a PR you cannot verify
  from the package is a PR that is not ready to submit.
