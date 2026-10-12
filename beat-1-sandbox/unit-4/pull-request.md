# Unit 4 - Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review
repo, and of the evaluation runs that produced `eval-run.txt`. This
file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own;
content placed under the wrong label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/154

**Branch**

`fix/60-none-chunk-text`

## Eval iterations

**Run history**

1. Full run: **19/20** — disagreed on `pkg-04` (gold reject / rubric accept).
2. Partial `--only pkg-04,pkg-02,pkg-10,pkg-07` after tightening `decisive-test`: **4/4**.
3. Full run: **20/20** (bar 18/20: PASS) — saved as `eval-run.txt` (model sonnet, 2026-10-12T06:51:18Z).

**Package analysis**

`pkg-04` (sharkdp/bat#3833, category `not-tested`). Gold label: **reject**. After the revise: my rubric **reject** (agree). The plan's decisive check is re-running `bat Cargo.toml` under pwsh with less-Windows and seeing colored paged output. The package only says "Tested locally… colors work now. `cargo test` passes" — no pasted repro transcript. That is vibes + suite, not the plan's end-to-end repro, so `decisive-test` fails and the package rejects.

**Check rationale**

Quoted from uploaded `tools/pr-precheck/rubric.md`:

> `| decisive-test | Candidate PR test-evidence section read against the plan's named test plan / repro steps; also any claim that repo checks were run. | Evidence pastes an observable run of the plan's named decisive repro (command or equivalent transcript) with a stated outcome (before/after or after-with-expected). Fail on vibes ("tested locally", "colors work now", "works on my machine"), on "tests pass" / suite-only with no pasted repro, on a control/unrelated path that never exercised the bug, or when the plan's named repro is never shown. A unit test for a helper is not enough when the plan's decisive check is an end-to-end repro. | required |`

Why it reads this way: the first full run accepted `pkg-04` because narrative "colors work" looked like an after-outcome. I revised the pass condition to require a pasted repro of the plan's named case, and to say helper unit tests / suite-only do not replace that. That matches the not-tested gold family without loosening plan-fidelity or diff-reviewable.

**Trade-offs**

Tightening `decisive-test` for `pkg-04` could have flipped a clear-accept that only shows suite output. I re-ran `--only pkg-04,pkg-02,pkg-10,pkg-07` as canaries (clear-accept + other not-tested rejects) before the confirming full 20/20 run. Nothing else flipped.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
