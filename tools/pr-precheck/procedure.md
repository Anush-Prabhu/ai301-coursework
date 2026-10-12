# Procedure: how this tool grades a PR package

## Read order

1. Read **repo-facts** first. Note PR template asks, CONTRIBUTING rules, and AI disclosure policy in one line (`silent`, `disclose-required`, or `ban`).
2. Read **issue** title/body and **thread highlights**. Record any explicit maintainer direction about cause, approach, files, or testing. If none, write `no maintainer direction`.
3. Read **plan context** before the candidate PR: scope pair (in / not-in), named files, approach, test plan, risks, and any deviation / shortfall notes. Write one line: "plan promises ___".
4. Read the **candidate PR title and description** next, as a stranger opening the PR would. Note fidelity claims, disclosures, template sections filled or skipped, and any deferred-scope language.
5. Read the **commit list**, then the **unified diff**. List changed paths and flag debris (debug, dead code, churn) and any hunk outside the plan's files/boundary.
6. Read **test evidence** last. Map each pasted run to the plan's named repro / expected outcome.
7. Do not grade any check until steps 1–6 are done. Fidelity and standards checks need plan+diff+description together; test checks need plan test plan before evidence.

## Evidence gathering

Pull a short working note per family before grading:

- **Plan fidelity:** From plan — boundary, files, deviations/shortfalls. From diff — changed paths + functional edits. From description — claims of exactness / completeness. Pair them: more-than-plan, less-than-plan, or claim≠diff.
- **Test evidence:** From plan — decisive repro and expected after. From test-evidence — what was actually run (before/after, suite). Flag control-only or unrelated-path runs.
- **Diff quality:** From diff/commits — leftover debug, commented attempts, dead helpers, formatting-only hunks, unrelated files.
- **Standards / comms:** From repo-facts — required template sections and AI policy. From description — filled sections, disclosure sentence, issue link/checklist/changelog. From diff — whatsnew/docs if template requires them in-tree.

Live mode only: gather issue/thread/template/policy via `gh` / API / web per `references/evidence-guide.md`; take plan from `plan.md` (including Deviations), diff from `git diff main...HEAD`, description from `pr_draft.md`, evidence from `test_evidence.md`. Eval mode: use only the bundle sections — never fetch.

## Check execution

Grade checks in this fixed order so two executors match:

1. `plan-fidelity`
2. `decisive-test`
3. `diff-reviewable`
4. `standards-met`
5. `commits-coherent` (preferred)

For each check:

1. Open only the evidence named in `rubric.md` for that check (use the working notes).
2. Apply the pass condition as written — outcome, not description length or commit count.
3. Grade `pass`, `fail`, or `unclear`. Use `unclear` only when the named evidence location is genuinely absent from the package, not when you skipped reading.
4. Attach a one-line evidence quote or fact that decided the grade.

Do not re-read the whole package between checks unless a prior grade exposed a contradiction you must verify.

## Verdict assembly

1. Apply the rubric verdict rule exactly: `accept` only if every required check is `pass`; else `reject`.
2. Treat every required `unclear` as `fail`.
3. Ignore `preferred` grades when choosing the verdict.
4. When quoting the deciding failure, use the **first failing required check in the execution order above**.
5. In the JSON output, list every check with its grade and one-line evidence.
6. Emit the fenced JSON block last, as `SKILL.md` requires.
