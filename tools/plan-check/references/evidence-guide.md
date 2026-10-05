# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- **Where it lives (eval):** `## Repro evidence` (steps, artifact, control) and the plan's diagnosis / cause paragraphs. Live: the student's posted repro comment on the issue, plus the draft `plan.md` diagnosis.
- **What good looks like:** The stated cause cites behavior the repro actually shows. A control that rules a layer out means a plan blaming that layer fails grounding.

## Scope

- **Where it lives (eval):** The candidate plan's scope / in-scope / not-in-scope / files list. Live: same sections in `plan.md`.
- **What good looks like:** One bounded change for this issue. Extra migrations, redesigns, new options, or multi-front campaigns are scope creep even if the core fix is also named.

## Executability

- **Where it lives (eval):** Plan approach + named files/areas. Live: `plan.md` approach and file list.
- **What good looks like:** A stranger can open a named file and start the chosen edit. "Investigate the stack" with no chosen layer is not executable.

## Test plan

- **Where it lives (eval):** Plan test-plan section, mapped to repro steps/artifact. Live: `plan.md` test plan vs posted repro steps.
- **What good looks like:** Names an observable pass condition for this bug (e.g. re-run the failing call / fixture and expect a score, not a TypeError). "Full suite" alone or "should feel fast" is not decisive.

## Honesty

- **Where it lives (eval/live):** Plan risks, unknowns, and `## Deviations`.
- **What good looks like:** Uncertainties labeled as unknowns; mid-build changes recorded under Deviations rather than silently diverging from the posted plan.

## Comms

- **Where it lives (eval):** `## Thread highlights` / issue context for maintainer direction; `## Repo facts` for templates and AI policy; candidate plan comment for engagement + disclosure. Live: issue thread + CONTRIBUTING/AI policy docs + draft comment.
- **What good looks like:** Explicit maintainer direction is engaged (followed or declined with reason). If policy requires AI disclosure, the comment names the tool and human review. Boilerplate that ignores an in-thread culprit file or required disclosure fails.
