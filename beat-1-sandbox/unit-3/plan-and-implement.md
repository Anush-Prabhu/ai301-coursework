# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Anush-Prabhu

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60#issuecomment-5986389310

~~~~
Diagnosis from the Unit 2 repro: `chunk.get("text", "")` still returns `None` when the key is present, so `" ".join(...)` in `FaithfulnessChecker.check` raises `TypeError: sequence item 0: expected str instance, NoneType found`. Control with a real string scores fine.

Plan: normalize with `(chunk.get("text") or "")` at that join in `rag/evaluator/faithfulness_checker.py` only. Not touching claim extraction or other scorers.

Test: re-run `FaithfulnessChecker().check('Knows Python.', [{'text': None}])` and expect a float in `[0.0, 1.0]`; unlock `test_none_context_chunk_text`.

Branch (on my fork): `fix/60-none-chunk-text`.

Drafted with AI assistance (Cursor); I reviewed the diagnosis against my posted repro and will run the before/after myself.
~~~~

---

## Your branch

**Branch**

fix/60-none-chunk-text

**Evidence**

Before (old join expression / pre-fix behavior):

```
>>> chunks=[{'text': None}]
>>> ' '.join([chunk.get('text', '') for chunk in chunks])
TypeError: sequence item 0: expected str instance, NoneType found
```

After (on branch `fix/60-none-chunk-text`, commit `b7bbf8a`):

```
$ set PYTHONPATH=.
$ python -c "from rag.evaluator.faithfulness_checker import FaithfulnessChecker; print(repr(FaithfulnessChecker().check('Knows Python.', [{'text': None}]))); print(repr(FaithfulnessChecker().check('Knows Python.', [{'text': 'Knows Python well'}])))"
0.0
1.0

$ python -m pytest tests/unit/test_faithfulness_checker.py::TestFaithfulnessChecker::test_none_context_chunk_text -q
.                                                                        [100%]
1 passed in 0.32s
```

Fork branch: https://github.com/Anush-Prabhu/pathreview-ai301-fa26-s1/tree/fix/60-none-chunk-text

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run against `tools/plan-check/` rubric + evidence-guide + procedure + SKILL: **20/20** scored items, category floor met (`clear-accept 7/7`, `scope-creep 4/4`, `thread-convention 2/2`, `unbuildable 3/3`, `wrong-cause 4/4`), bar PASS. Matches committed `beat-1-sandbox/unit-3/eval-run.txt` (`agreement: 20/20 scored items  (bar: 18/20: PASS)`).

**Package analysis**

Package: `pkg-01` (category `wrong-cause`, source httpie/cli#1838).

- Gold verdict: `reject`
- Skill verdict: `reject` (agree)

Repro control (quoted from the package):

> Control run, same venv, same items, no `-v` flag: … prints `header1: xyz` / `{"x": "1"}` … `--debug` … error is raised by argparse's `parse_args` while consuming positionals; the request items are never handed to HTTPie's item parser.

Plan diagnosis (quoted):

> The `REQUEST_ITEM` tokenizer in `httpie/cli/requestitems.py` is the problem. … The Python-version difference is a red herring; the tokenizer has always been too strict about colon items.

Deciding check: `diagnosis-grounded` → `fail`. The control already shows the same request items parse when `-v` is absent, and `--debug` pins argparse before the item parser runs, so blaming the tokenizer contradicts the package's own evidence. Required fail → verdict `reject`.

**Check rationale**

Quoted from uploaded `tools/plan-check/rubric.md`:

> `| \`diagnosis-grounded\` | The plan's stated cause / diagnosis, read side-by-side with the package's repro-evidence block (steps, artifact, and any control run that isolates the subject). | The diagnosis follows from what the repro evidence shows. Fail when the plan blames a component the package's own control already ruled out, ignores a control that isolates a different cause, or contradicts the pasted artifact. | required |`

Why: the gold set's `wrong-cause` family (pkg-01, pkg-07, pkg-11, pkg-16, calib-03) all pass a polished wrong diagnosis unless the grader is forced to read the control/artifact first. This check is required so those packages reject.

**Trade-offs**

`diagnosis-grounded` will miss a plan whose diagnosis is wrong for reasons that never appear in the package (e.g. live-only knowledge). That is accepted: eval mode's world is the bundle. Loosening it to "sounds plausible" would flip wrong-cause packages to false accepts; canaries for that change are any agreeing `wrong-cause` row and calib-03.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
