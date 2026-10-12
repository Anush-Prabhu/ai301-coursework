# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `plan-fidelity` | Side-by-side: plan context (in-scope / not-in-scope / files / approach / deviation notes) vs the candidate PR's unified diff (changed paths and functional hunks) vs the description's fidelity claims ("exactly as planned", "no changes beyond…", "docs now document…"). | Every functional change in the diff falls inside the plan's stated boundary or is named in a deviation note, and the description does not claim more or less than the diff delivers. Fail when the diff adds unrequested options/rewrites/files, when planned work is missing with no honest shortfall note in plan+description, or when the description claims fidelity the diff contradicts. An honest shortfall that the plan and description both disclose as deferred is a pass. | required |
| `decisive-test` | Candidate PR test-evidence section read against the plan's named test plan / repro steps; also any claim that repo checks were run. | Evidence pastes an observable run of the plan's named decisive repro (command or equivalent transcript) with a stated outcome (before/after or after-with-expected). Fail on vibes ("tested locally", "colors work now", "works on my machine"), on "tests pass" / suite-only with no pasted repro, on a control/unrelated path that never exercised the bug, or when the plan's named repro is never shown. A unit test for a helper is not enough when the plan's decisive check is an end-to-end repro. | required |
| `diff-reviewable` | Candidate PR unified diff and commit list. | The fix is visible and not buried by debris: no debug prints left in, no commented-out attempts/dead helpers, no pure formatting/import churn hunks, no unrelated drive-by edits folded into the same PR. Fail when debris or unrelated hunks are present even if the core fix is correct. | required |
| `standards-met` | Repo-facts (PR template asks, CONTRIBUTING, stated AI policy) vs candidate PR description (and title) vs diff where template asks for changelog/whatsnew entries. Treat every eval package as AI-assisted work. | Required template sections are filled with real content (not empty/boilerplate that skips asks); if policy requires AI disclosure, the description discloses tool + human review; issue linkage / checklist / changelog asks present in repo-facts are met when required. Fail when a required ask is visibly ignored. Pass when policy/template is silent on a soft optional ask. | required |
| `commits-coherent` | Candidate PR commit list read against the diff. | Commit subjects describe the intended fix rather than only `wip` / `fix` / `fmt + cleanup` noise that signals unfinished debris. Preferred only — never holds an otherwise ready package. | preferred |

## Verdict rule

`accept` (ready to submit) only if every `required` check is `pass`.

One required `fail` yields `reject` (hold).

`unclear` on a required check counts as `fail`: a PR whose needed evidence is missing from the package is not ready to submit.

`preferred` checks never change the verdict; report their grades only.
