# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- **Where it lives (eval):** `## Plan context` (scope, files, approach, test plan, deviation/shortfall notes) paired with `### Diff` and the description's fidelity claims under `### Description`. Live: `plan.md` (including `## Deviations`) vs `git diff main...HEAD` vs `pr_draft.md` body.
- **What good looks like:** Every functional hunk sits inside the plan's boundary or a written deviation. Description claims match the diff. Silent extras (new flags, rewrites, unrelated files) fail; silent missing work fails; claiming "docs updated" / "exactly as planned" when the diff disagrees fails. Honest deferral named in both plan and description passes.

## Test evidence (harness category: not-tested)

- **Where it lives (eval):** Plan context test plan + `### Test evidence`. Live: `plan.md` test plan vs `test_evidence.md` (and any pasted suite output).
- **What good looks like:** A pasted run of the plan's named decisive repro (command/transcript) with before/after or after-with-expected. "Tests pass", "tested locally", "colors work now", "works on my machine", or only a control/unrelated path is not decisive. Helper unit tests do not replace an end-to-end repro the plan named.

## Diff quality (harness category: unreviewable)

- **Where it lives (eval):** `### Diff` and `### Commits`. Live: `git diff main...HEAD` and `git log main..HEAD --oneline`.
- **What good looks like:** The fix is readable without digging past debug prints, commented-out attempts, dead helpers, formatting/import churn, or drive-by edits. Debris present means fail even when the core fix is right.

## Standards and comms (harness category: standards-wall)

- **Where it lives (eval):** `## Repo facts` (template, CONTRIBUTING, AI policy) vs `### Description` / title, and the diff when template asks for changelog/whatsnew in-tree. Live: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md` / AI policy, `pr_draft.md`.
- **What good looks like:** Required template sections have real content; required AI disclosure names tool + human review; required issue link / checklist / changelog asks are met. Soft-optional unmet asks do not fail. (Whether description claims match the diff is plan fidelity, above.)
