# Voice guide: how I talk upstream

## Who I am in threads

I am Anush Prabhu, working through AI301 on Path Review. I write Python
daily (FastAPI, pytest, RAG pipelines) but this is my first contribution
to a repo I did not already own. Readers can expect that anything I
state as fact, I ran — and anything I have not run, I mark as a guess.

## Rules I write by

### Rule: promise investigation, never a date or a guaranteed PR

A claim commits me to looking and reporting back. It does not commit me
to a fix, a weekend deadline, or a result I have not seen yet.

- Wrong: "I'll take this and have a PR up by Friday."
- Right: "I'd like to take this. I'll reproduce the TypeError on current main and report what I find here either way."

### Rule: paste the artifact, do not narrate it

If I say something crashes or is missing, the output that shows it is in
the comment. A reader should never have to take my word for a run I
could have pasted.

- Wrong: "Confirmed, FaithfulnessChecker crashes on None text."
- Right: "`FaithfulnessChecker().check('Knows Python.', [{'text': None}])` raises `TypeError: sequence item 0: expected str instance, NoneType found`."

### Rule: put environment limits next to the result

Caveats sit beside the finding, not in a later reply after someone asks.

- Wrong: "Reproduced on my machine."
- Right: "Reproduced on Windows 11, Python 3.14.5, repo at commit `<sha>` on `main`."

### Rule: no filler enthusiasm

I do not open with praise for the project or close with "happy to help
however I can." Neither carries information.

- Wrong: "Great project! Happy to help with anything!"
- Right: (nothing — the comment starts at the first informative sentence)

### Rule: AI assistance disclosed when the repo asks, otherwise said plainly in course work

Path Review is AI-assisted coursework by design. When a repo's policy
requires disclosure, I name the tool and that I reviewed the output. I
do not hide assistance behind a polished voice.

- Wrong: (silent on AI when the policy requires disclosure)
- Right: "Drafted with AI assistance (Cursor); I ran the reproduction myself and edited the comment."

## Things I never post

- A date, an estimate, or "should be quick."
- A root cause written as fact when I have only a guess.
- "Same here" / "+1" with no artifact of my own.
- Piggybacking on a classmate's repro ("can confirm, same as above").
- A claim on an issue whose thread I have not read to the end.
