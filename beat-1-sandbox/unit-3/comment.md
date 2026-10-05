Diagnosis from the Unit 2 repro: `chunk.get("text", "")` still returns `None` when the key is present, so `" ".join(...)` in `FaithfulnessChecker.check` raises `TypeError: sequence item 0: expected str instance, NoneType found`. Control with a real string scores fine.

Plan: normalize with `(chunk.get("text") or "")` at that join in `rag/evaluator/faithfulness_checker.py` only. Not touching claim extraction or other scorers.

Test: re-run `FaithfulnessChecker().check('Knows Python.', [{'text': None}])` and expect a float in `[0.0, 1.0]`; unlock `test_none_context_chunk_text`.

Branch (on my fork): `fix/60-none-chunk-text`.

Drafted with AI assistance (Cursor); I reviewed the diagnosis against my posted repro and will run the before/after myself.
