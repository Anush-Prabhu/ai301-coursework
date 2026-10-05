# Plan: FaithfulnessChecker TypeError on chunk text None (#60)

## Diagnosis

`FaithfulnessChecker.check` builds context with:

```python
context_text = " ".join([chunk.get("text", "") for chunk in context_chunks])
```

`dict.get("text", "")` only substitutes the default when the key is **missing**. When the key is present and the value is `None`, `.get` returns `None`, and `" ".join(...)` raises:

`TypeError: sequence item 0: expected str instance, NoneType found`

Unit 2 reproduction pinned this on `main` @ `f89c06fc3ff292df2a04a39ac51319d32a76b779`: the None-text call crashes; a control chunk with a real string returns `1.0`.

## Scope

**In scope**
- Normalize falsy/`None` chunk `text` to `""` at the join site in `rag/evaluator/faithfulness_checker.py` so `check` always joins strings.
- Keep/unlock the existing xfail test `test_none_context_chunk_text` in `tests/unit/test_faithfulness_checker.py` so it asserts a float score in range.

**Not in scope**
- Changing claim extraction, stop-word logic, or other evaluators (`relevance_scorer`, etc.).
- Broader schema validation for chunk dicts.

## Files

- `rag/evaluator/faithfulness_checker.py` — join site only
- `tests/unit/test_faithfulness_checker.py` — remove strict xfail once behavior matches (or leave xfail removed after fix)

## Approach

1. Replace the join comprehension with an explicit normalize, e.g. `(chunk.get("text") or "")`, so both missing keys and `None` become empty strings.
2. Re-run the None-text call and the existing unit test.
3. Confirm the control path (real string text) still returns a float score.

## Test plan

**Before (failing):**

```python
from rag.evaluator.faithfulness_checker import FaithfulnessChecker
FaithfulnessChecker().check('Knows Python.', [{'text': None}])
```

Expect: `TypeError`.

**After (passing):**

Same call returns a `float` in `[0.0, 1.0]` with no exception.

Also: `pytest tests/unit/test_faithfulness_checker.py::TestFaithfulnessChecker::test_none_context_chunk_text -q` passes (xfail removed).

Control unchanged: `[{'text': 'Knows Python well'}]` still scores without error.

## Risks / unknowns

- Empty context after normalizing all-None chunks already returns `0.0` via the empty-input / empty-claims paths — confirm that remains acceptable.
- No other call sites assumed; only this join is changed.

## Deviations

nothing changed; the plan held
