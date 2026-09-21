# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60

**Verdict output**

~~~~
issue-select live mode on 3 Path Review candidates
(scope: codepath/pathreview-ai301-fa26-s1; Path Review house rule: classmate claim comments do not block)

Ranked accepts (fit order):
1. #60 Faithfulness checker crashes when a context chunk has text: None
   fit: tier-1 RAG bug with a one-line repro; matches Python/RAG preference and a week-sized fix
2. #53 PII scrubber fails to redact parenthesized US phone numbers
   fit: clear safety regex bug; slightly less central to the RAG work I want next
3. #62 Health check references settings.redis_host, which does not exist on Settings
   fit: bounded API config bug; less interesting than the faithfulness path

Rejected: none among these three (all required checks passed under the Path Review house rule).

--- #60 ---
not-archived: pass — archived: no
recent-default-branch-activity: pass — 2026-09-16 commit on main within 180 days of today
repo-still-shipping: pass — last push 2026-09-16; no releases published, push clause carries liveness
scope-is-one-shippable-change: pass — single TypeError in FaithfulnessChecker.check when chunk text is None; named failing test path
not-actively-claimed: pass — assignees none; no open linked PRs; no claim comments on this issue (house rule would ignore classmate claims anyway)
ai-contribution-allowed: pass — docs/CONTRIBUTING.md states no AI ban (silence)
newcomer-signposted: pass — labels include good first issue; tier-1
verdict: accept

--- #53 ---
not-archived: pass — archived: no
recent-default-branch-activity: pass — recent main commits within 180 days
repo-still-shipping: pass — last push within 180 days
scope-is-one-shippable-change: pass — extend phone regex for parenthesized US format; named scrub/detect behavior
not-actively-claimed: pass — assignees none; no open linked PRs; no claim comments
ai-contribution-allowed: pass — no AI ban in contribution docs
newcomer-signposted: pass — good first issue; tier-1; safety
verdict: accept

--- #62 ---
not-archived: pass — archived: no
recent-default-branch-activity: pass — recent main commits within 180 days
repo-still-shipping: pass — last push within 180 days
scope-is-one-shippable-change: pass — health Redis probe should use settings.redis_url instead of missing redis_host/port
not-actively-claimed: pass — assignees none; no open linked PRs; no claim comments
ai-contribution-allowed: pass — no AI ban in contribution docs
newcomer-signposted: pass — good first issue; tier-1; api
verdict: accept

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-09-16 default-branch commit within 180 days"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "last push 2026-09-16; releases none published"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "single TypeError when chunk text is None; clear repro"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; no open linked PRs; no claim comments"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: no AI ban (silence)"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "good first issue, rag, tier-1"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "recent main commits within 180 days"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "last push within 180 days"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "extend phone regex for (555) 123-4567"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; no open linked PRs"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: no AI ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "good first issue, safety, tier-1"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "recent main commits within 180 days"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "last push within 180 days"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "use settings.redis_url in health Redis probe"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; no open linked PRs"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: no AI ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "good first issue, api, tier-1"}
    ],
    "verdict": "accept"
  }
]
```
~~~~

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Full run against the filled rubric in `~/.claude/skills/issue-select/rubric.md`: agreement **20/20** scored items (bar: 18/20: PASS); categories claimed 4/4, clear-accept 8/8, dead-repo 3/3, policy 1/1, scope 4/4. That run is the transcript committed as `eval-run.txt` (header agreement line: `agreement: 20/20 scored items  (bar: 18/20: PASS)`).

**Issue analysis**

`issue-12` (bookwyrm-social/bookwyrm#1133). Gold label: **reject**. My rubric: **reject**. Every liveness, shipping, scope, and claim check passed — recent commits, recent release, bounded UI enhancement, unclaimed — but `ai-contribution-allowed` failed on the contribution-policy line: *"We do not accept AI-generated code or documentation."* That required fail forces reject under the verdict rule, which matches the gold `policy` category.

**Check rationale**

From uploaded `tools/issue-select/rubric.md`:

> `| ai-contribution-allowed | The "contribution policy" line in repo facts (including any Generative AI / AI use section quoted there, and any AI_POLICY / AGENTS.md note). | The policy does not ban AI-generated or AI-assisted contributions outright. An explicit ban fails. Disclosure, "understand and test what you submit", and human-review requirements **pass** — those are terms to follow, not walls. Silence passes: most repos state nothing, and nothing is not a restriction. "Strongly discourage" language that still allows human-reviewed AI assistance also passes. | required |`

I wrote it this way because the course contribution workflow is AI-assisted, so an outright ban is a hard dead end even when the issue looks perfect. Conditions (disclose / understand / test) stay as pass so repos like conda and zulip are not rejected for having a policy at all.

**Trade-offs**

This check rejects `issue-12` even though it would otherwise be a strong first issue. It deliberately does **not** fail tldr-pages style "strongly discourages generative AI … without human review" language (`issue-10` still rejects on scope as a megaissue, not on policy). I accept that a repo with a soft cultural vibe against AI but no written ban will still pass — silence and soft discouragement are not the same as a ban, and the evidence guide says silence passes.

---

## Selection rationale

**Selection rationale**

1. **Fit / time:** `#60` is a tier-1 RAG bug with a one-line Python repro (`FaithfulnessChecker().check(..., [{'text': None}])`). It matches the RAG work I already know and looks like a same-week fix: guard `None` text, keep the join happy, drop any related xfail if present.

2. **What the verdict got right / what I weighed:** The skill correctly accepted it on every required check (alive repo, bounded crash, unclaimed, AI policy silent). Separately I weighed that the failing path is in `rag/evaluator/` — closer to the systems I want to practice than the phone-regex (`#53`) or Redis URL (`#62`) alternatives, which also accepted.

3. **Claim difficulty:** Nobody has commented or linked a PR on `#60` yet. Path Review expects a claim comment in Unit 2; I am not claiming here. Shared classroom issues are normal under the house rule, so the main risk is timing — another student may claim before I post in Unit 2.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
