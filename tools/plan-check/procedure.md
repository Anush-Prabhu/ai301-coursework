# Procedure: how this skill grades a plan package

## Read order

1. Read the **issue context** (title, body, labels) and note the subject behavior in one line.
2. Read **thread highlights** / maintainer comments next. Record any explicit direction about cause, approach, files, or testing. If none, write `no maintainer direction`.
3. Read the **repo-facts** block. Record contribution / AI disclosure policy in one line (`silent`, `disclose-required`, or `ban`).
4. Read the **repro-evidence** block before the plan. Note: environment, steps, artifact, and any **control** run that isolates the subject. Write one sentence: "evidence pins ___".
5. Read the **candidate plan** (diagnosis, scope, files, approach, test plan, risks/unknowns, deviations).
6. Read the **candidate plan comment** last, as a stranger on the thread would.
7. Do not grade any check until steps 1–6 are done. Grounding checks depend on repro-before-plan order; comms checks depend on thread/policy before the comment.

## Evidence gathering

For each family, pull facts into a short working note before grading:

- **Diagnosis / grounding:** From repro-evidence — artifact text + control outcome. From plan — the stated cause sentence(s).
- **Scope:** From plan — in-scope, not-in-scope, file list, extra campaigns (migrations, rewrites, new options).
- **Executability:** From plan — named files/paths, chosen approach (not a menu of undecided options).
- **Test plan:** From plan — how success is observed. From repro-evidence — the failing step/artifact that should flip.
- **Honesty:** From plan — risks, unknowns, deviations headings.
- **Comms / thread:** From issue thread highlights — explicit maintainer asks. From plan comment — whether those asks are engaged.
- **Comms / AI policy:** From repo-facts — disclosure rule. From plan comment — disclosure sentence if any.

Live mode only: gather issue + thread via `gh` / API / web per `references/evidence-guide.md`; take repro evidence from the student's posted repro comment (or house repro quoted in the drafts). Eval mode: use only the bundle sections above — never fetch.

## Check execution

Grade checks in this fixed order so two executors match:

1. `diagnosis-grounded`
2. `scope-bounded`
3. `executable`
4. `decisive-test`
5. `thread-aware`
6. `ai-disclosure`
7. `unknowns-honest` (preferred)

For each check:

1. Open only the evidence named in `rubric.md` for that check (use the working notes).
2. Apply the pass condition as written — outcome, not write-up length or heading count.
3. Grade `pass`, `fail`, or `unclear`. Use `unclear` only when the named evidence location is genuinely absent from the package, not when you skipped reading.
4. Attach a one-line evidence quote or fact that decided the grade.

Do not re-read the whole package between checks unless a prior grade exposed a contradiction you must verify.

## Verdict assembly

1. Apply the rubric verdict rule exactly: `accept` only if every required check is `pass`; else `reject`.
2. Treat every required `unclear` as `fail`.
3. Ignore `preferred` grades when choosing the verdict.
4. In the JSON output, list every check with its grade and one-line evidence. The deciding required fail (if any) must be quotable from that list.
5. Emit the fenced JSON block last, as `SKILL.md` requires.
