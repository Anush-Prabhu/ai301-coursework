# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `diagnosis-grounded` | The plan's stated cause / diagnosis, read side-by-side with the package's repro-evidence block (steps, artifact, and any control run that isolates the subject). | The diagnosis follows from what the repro evidence shows. Fail when the plan blames a component the package's own control already ruled out, ignores a control that isolates a different cause, or contradicts the pasted artifact. | required |
| `scope-bounded` | The plan's in-scope / not-in-scope statements and the files or areas it names for the change. | The change is one shippable fix for this issue. Fail when the plan wraps the fix in a redesign, migration, cross-cutting rewrite, new option/framework, multi-front campaign, or "while we're here" work the issue did not ask for. | required |
| `executable` | The plan's approach section: named files/areas, concrete steps or edit sites a stranger could open and start changing. | A stranger who has only the package could begin the build without asking the author what to edit or which approach to pick. Fail when files/areas are missing, the approach is "investigate" with no chosen layer, or every real decision is deferred to build time. | required |
| `decisive-test` | The plan's test plan, read against the repro evidence's steps and artifact. | Names an observable outcome that would show this issue is fixed (re-run of the failing case with an expected result, a named assertion, a decisive fixture). Fail when the test is vibes ("should feel fast"), only "run the full suite" with no outcome for this fix, or "nothing else should break" with no positive check. | required |
| `thread-aware` | The plan comment (and plan, if it cites thread) read against thread highlights / maintainer direction in the issue context, when any explicit direction is present. | If the thread contains explicit maintainer direction about cause, approach, or what to test, the package engages that direction (follows it, or names why not). Fail when such direction is present and the comment/plan ignores it. Pass when the thread has no such direction to engage. | required |
| `ai-disclosure` | The plan comment read against the repo-facts contribution / AI policy. Treat every eval package as AI-assisted work. | If the stated policy requires disclosing AI usage, the comment discloses tool and that a human reviewed. Fail when disclosure is required and absent. Pass when the policy is silent or only soft-optional and unmet soft asks are not hard requirements. | required |
| `unknowns-honest` | The plan's risks / unknowns / deviations language. | Uncertainty is labeled as such rather than stated as settled fact. Preferred only — never holds an otherwise ready package. | preferred |

## Verdict rule

`accept` (ready to post and build from) only if every `required` check is `pass`.

One required `fail` yields `reject` (hold).

`unclear` on a required check counts as `fail`: a plan whose needed evidence is missing from the package is not ready to build from.

`preferred` checks never change the verdict; they only rank packages that already accept.
