# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Anush-Prabhu

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60#issuecomment-5819968403

~~~~
I'd like to take this. I'll reproduce the `TypeError` from `FaithfulnessChecker.check` when a chunk has `text: None` on current `main` and report what I find here either way.

Drafted with AI assistance (Cursor); I ran / will run the reproduction myself and edit before posting.
~~~~

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60#issuecomment-5819970239

~~~~
## Reproduction

**Environment**
- OS: Windows 11 (NT 10.0.26200)
- Under test: `codepath/pathreview-ai301-fa26-s1` @ `main`, commit `f89c06fc3ff292df2a04a39ac51319d32a76b779` (2026-09-16)
- Interpreter: Python 3.14.5
- Extra: `structlog` installed so the module imports; no other project deps needed for this call path

**Steps**

```python
from rag.evaluator.faithfulness_checker import FaithfulnessChecker
FaithfulnessChecker().check('Knows Python.', [{'text': None}])
```

**Observed (failing run)**

```
TypeError: sequence item 0: expected str instance, NoneType found
```

The join in `check()` uses `chunk.get("text", "")`, so a present key with value `None` returns `None` and `" ".join(...)` raises.

**Control (same session)**

```python
FaithfulnessChecker().check('Knows Python.', [{'text': 'Knows Python well'}])
# returns 1.0 — no exception
```

**Expected:** treat `None` text like a missing key (empty string) and return a score.
**Actual:** `TypeError` before any scoring.

Drafted with AI assistance (Cursor); I ran this reproduction myself on the commit above and edited the comment.
~~~~

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run against the filled rubric + evidence guide in `~/.claude/skills/repro-check/`: agreement **20/20** scored items (bar: 18/20: PASS); categories clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4. That run is the transcript committed as `eval-run.txt` (agreement line: `agreement: 20/20 scored items  (bar: 18/20: PASS)`).

**Package analysis**

`pkg-20` (ghostty-org/ghostty#13604). Gold label: **reject**. My rubric: **reject**. The repro itself is excellent on env, steps, and artifact-matches-issue — but `conventions-respected` failed because repo facts require disclosing all AI usage (`CONTRIBUTING.md` + `AI_POLICY.md`) and neither the claim nor the repro comment discloses. That required fail forces reject, which is exactly the one-item `disclosure` category the floor exists for.

**Check rationale**

From uploaded `tools/repro-check/rubric.md`:

> `| conventions-respected | The contribution-policy line in repo facts, plus any stated template or AI-disclosure ask. | The package meets the repo's stated asks. Where the policy requires disclosing AI assistance, the posted text discloses it. An outright ban on AI-assisted work fails the package. Silence passes. Soft "disclose if you used AI" language that is unmet fails. | required |`

I wrote it this way so the disclose-or-hold wall (pkg-20) is visible without rejecting repos that say nothing (silence passes) or that only ask for human review of AI output. Course packages are AI-assisted by design, so a required disclosure that is missing is a hold, not a style note.

**Trade-offs**

This check rejects `pkg-20` even though every proof-family check would pass. I accept that a polished package with an unspoken AI draft still fails when the policy demands disclosure — that is the point of the category floor. Soft “strongly discourage without human review” language without a hard disclose requirement still passes on this check (and may reject for other reasons).

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
