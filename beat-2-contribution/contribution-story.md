# Contribution: OCSF ingest drops actor, session, cloud and device fields

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Anush Prabhu
**GitHub Username:** Anush-Prabhu
**Issue:** https://github.com/koda-ai-studio/agent-bom/issues/5956
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout, rewrote the empty pytest query, and dropped OWNER-filed and non-bug hits after the first shortlist filled with practice repos**

I overlaid issue-scout on the Unit 1 skill (kept `rubric.md`) and wrote three `gh search issues` queries from the fit profile: Python `good first issue`, Python `help wanted`+`bug`, and Python `bug`+`pytest`, ranked by drop-assignee / drop-OWNER / fewest comments. The first Q3 (`RAG OR FastAPI OR ...` with `good first issue`) returned `[]`, and fewest-comments still put 0-comment persona cards in the top five; I rewrote Q3 to `--label bug pytest` and dropped results without a `bug` label. The second scan graded five issues: four accept (agent-bom#5956, Yawnalyzer#14, phantom#82, crosstl#2799) and one reject (repowise#4608, open PR #4625). I did not add a required stars check — gold `issue-06` is a 37-star clear-accept — so 2-star and 4-star repos still pass, which I logged in `scan-notes.md`.

**Unit 6: Installed the voice-guard, patched scope-feasible, claimed agent-bom#5956, wrote CLAUDE.local.md**

I installed the voice-guard (canonical guide at `~/.claude/voice-guard/voice-guide.md`, hook on PreToolUse) and replaced repro-check / plan-check scopes with the wild copies. `ln -s` is not available on this Windows box, so the filled guide is copied into each skill folder, and the hook uses `pythoncore-3.14-64\python.exe` because `python3` on PATH is a WindowsApps stub. The wiring test stopped `gh issue comment --help` with "no body the guard can read"; `check_voice.py --draft claim-draft.md` passed, then I posted the claim. `CLAUDE.local.md` is in the fork clone and listed in `.git/info/exclude` (`git status` does not show it).

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

Last week's scan accepted four Python bugs. On 2026-10-25 I replaced `scope-is-one-shippable-change` with `scope-feasible` and graded those four again. All four still accept. Difficulty: Yawnalyzer#14 straightforward, agent-bom#5956 and phantom#82 moderate, crosstl#2799 ambitious (Mojo `global_idx` mapping). I picked koda-ai-studio/agent-bom#5956: `_normalize_ocsf_event` drops actor, session, cloud, and device on OCSF ingest. It is one Python API function with a named file, `help wanted`, no assignee and no comments, and it sits on the API / safety side of my profile. CONTRIBUTING.md allows coding agents if I own the lines and add a regression test. I hope to learn how this repo keeps ingest metadata bounded without losing identity fields.

The scout was right that #5956 is one piece of work and still free. It was wrong last week to treat every open edge as a reject-shaped scope check — that is why I patched the row. It still cannot see star counts at search time, so 2-star and 4-star accepts stay in the shortlist; I left that as preferred-not-required because gold `issue-06` is 37 stars.

Claim comment: https://github.com/koda-ai-studio/agent-bom/issues/5956#issuecomment-6399207854

**Toolkit**

- Tool: issue-scout in direct grade mode on last week's four accepts, after the `scope-feasible` patch
- What it produced: all four accept; #5956 moderate. I claimed #5956.
- Difficulties: `scope-is-one-shippable-change` would have treated fixture lists and unnamed extra files as a fail; search still cannot see stars
- What changed: 2026-10-25 replaced `scope-is-one-shippable-change` with `scope-feasible` and added the difficulty-note section. Open edges are now notes, not rejects.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

Windows 11 (10.0.26300). Fork `Anush-Prabhu/agent-bom`, `main` at `43be104`. `uv` created a `.venv` with CPython 3.12.15; `uv sync --extra dev` installed the package and pytest. Host Python is 3.14.5; I ran the repro through the venv, not the host. First import of `agent_bom.api.observability_events` took about 30 seconds (FastAPI and the rest of the API package). No other setup fights.

**Steps to Reproduce**

1. From the clone at `43be104`, `uv sync --extra dev`.
2. Run `.venv/Scripts/python.exe` importing `_normalize_ocsf_event` on an event with `actor.user.name`, `actor.session.uid`, `cloud.account.uid`, `device.hostname`, and `observables[0].trace_id`.
3. Observed: `agent_name=''`, `session_id=''`, `trace_id='trace-abc'`. Returned keys have no actor/cloud/device.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** at `43be104`:

```
agent_name= ''
session_id= ''
trace_id= 'trace-abc'
keys= ['agent_name', 'detector', 'event_id', 'event_timestamp', 'event_type', 'message', 'ocsf_class_name', 'ocsf_class_uid', 'request_id', 'session_id', 'severity', 'source_id', 'tenant_id', 'tool_name', 'trace_id']
```

Lines 145–146 of `src/agent_bom/api/observability_events.py` are `"agent_name": ""` and `"session_id": ""`.

- **My findings:** The normalizer on current main still drops actor/session/cloud/device. I did not call the HTTP ingest path, so I did not see the issue's `runtime-<uuid4>` session id; that is `_runtime_observation_from_event`, not this function. I am not posting this report on the issue.

**Toolkit**

- Tool: repro-check rubric (wild scope) plus `check_voice.py --draft` on the claim; I held `claim-draft.md` and `repro-draft.md` against the claim-only then full-package checks
- What it produced: claim passed voice-guard and `claim-is-specific` (named `_normalize_ocsf_event` and the file). Repro shows the empty agent/session on `43be104`.
- Difficulties: the issue's uuid4 session is on the persist path; a normalizer-only run cannot show it
- What changed: nothing in the tool. The report stays at the function the issue names; ingest can wait until I write a regression test.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
