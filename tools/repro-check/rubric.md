# Rubric: is this reproduction package ready to post?

<!--
Proof families for Unit 2: environment recorded, steps a stranger can
re-run, artifact matches the issue (not an adjacent failure), outcome
stated honestly, and comments respect the repo's conventions.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| `env-recorded` | The repro report's environment record, read against any version claims in the issue or repo-facts block. | Names the OS, the version of the software under test (release tag, commit SHA, or branch plus a dated commit), and any dependency version the behavior actually routes through. "Latest" / "current main" alone fail — they are moving targets. A dependency version is owed only when the path runs through that dependency. | required |
| `steps-rerunnable` | The steps section of the repro report, read as if by a stranger who has only the public repo. | Every input needed to reach the reported state is in the report or reachable from a public link: commands as run, fixture/file contents inline or publicly linked, and starting state. Fails when any input lives somewhere the reader cannot reach (private repo, unshared config, "my usual setup"). Three terse complete lines pass. | required |
| `artifact-matches-issue` | The pasted artifact (error text, command output, listing, measurement) read side-by-side with what the issue describes. | The artifact shows **this issue's** subject. Fails when it shows an adjacent/self-inflicted result (different error or code path, a version the issue does not concern, or a state the reporter's own edit created), or when it only proves the software starts (banner, session list) without touching the subject. | required |
| `outcome-honest` | The report's stated conclusion, read against its own artifact. | The conclusion matches what the artifact shows. An evidenced cannot-reproduce passes in full (real attempt + env + steps + observed non-failure). A confident root-cause claim with no supporting artifact fails, as does a "confirmed" that the artifact does not support. | required |
| `claim-is-specific` | The candidate claim comment, read against the issue text. | Names something only a reader of *this* issue could write (specific behavior, file, or gap) plus a concrete next step. Fails if the comment would read identically on any other tracker issue ("please assign me"). A claim promises investigation and a report back — not a guaranteed fix or a date. | required |
| `conventions-respected` | The contribution-policy line in repo facts, plus any stated template or AI-disclosure ask. | The package meets the repo's stated asks. Where the policy requires disclosing AI assistance, the posted text discloses it. An outright ban on AI-assisted work fails the package. Silence passes. Soft "disclose if you used AI" language that is unmet fails. | required |
| `reader-effort-low` | Ordering of the report and whether the artifact is pasted or only described. | Reader meets environment → steps → artifact → conclusion, with the artifact pasted rather than summarized. Preferred only — never holds an otherwise ready package. | preferred |

## Verdict rule

`accept` (ready to post) only if every `required` check is `pass`. One required `fail` yields `reject` (hold).

`unclear` on a required check counts as `fail`: proof I cannot verify from the package is not ready to post.

`preferred` checks never change the verdict; they only rank packages that already accept.
