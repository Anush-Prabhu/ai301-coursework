# Scan, 2026-10-25

issue-scout live scan (scope: any public repo; claims count; fit profile: Python bugs in API / tests / ingestion / safety)

Queries: q1 `--label "good first issue" --language python`; q2 `--label "help wanted" --label bug --language python`; q3 `--label bug --language python pytest`. Each `--state open --limit 100`. Combined 300 hits, 298 unique.

Ranking: drop assignees, `codepath/` repos, `OWNER` authorAssociation, frontend/ci labels, missing `bug` label, `updatedAt` older than 90 days; fewest comments first (ties keep search order, not newest); one issue per repo; top 5.

Dropped 149 OWNER, 43 assigned, 27 non-bug, 4 frontend/ci, 4 stale. 71 survivors. **4 accepted, 1 rejected.**

## Accepted (fit order)

### 1. [koda-ai-studio/agent-bom#5956](https://github.com/koda-ai-studio/agent-bom/issues/5956)

fix(observability): OCSF ingest drops actor, session, cloud and device fields

- **From:** q2 (Python, `help wanted` + `bug`). 0 comments, no assignee, updated 2026-10-24.
- **Work:** `_normalize_ocsf_event` in `api/observability_events.py` hard-codes empty agent/session; map actor/cloud/device and make session ids deterministic; fixtures for OCSF classes 2004 and 6003.
- **Fit:** Python API ingest on an AI/MCP security scanner. Closest of the five to the API / safety sentence in the profile.
- **Query / rank signals:** q2; unassigned; `bug`; 0 comments; first issue from this repo.

### 2. [DepressionCenter/Yawnalyzer#14](https://github.com/DepressionCenter/Yawnalyzer/issues/14)

Keep survey answers that lack a colon from overwriting the previous question

- **From:** q2. 0 comments, no assignee, updated 2026-10-25.
- **Work:** one `else` branch in `Yawnalyzer_Step1_Intial_Cleaning.py` reuses `quest_name`; skip empty cells; add a test row with a trailing empty field. Named `NameError` when it is the first answer.
- **Fit:** named crash plus a test row. Repo is 2 stars; the rubric still accepts it (see scan-notes).
- **Query / rank signals:** q2; unassigned; `bug`; 0 comments.

### 3. [hayagrivai-labs/phantom#82](https://github.com/hayagrivai-labs/phantom/issues/82)

verify shares the real stdin between the two programs: identical programs are reported as different

- **From:** q2. 0 comments, no assignee, updated 2026-10-23.
- **Work:** `compare_behavior` / `execute_host_program` inherit real stdin; feed the same bytes to both sides; pytest acceptance is in the issue. Repo created 2026-10-21 (4 stars).
- **Fit:** pytest-shaped bug with a one-line repro (`echo alice | phantom verify ask.py ask.py`). Brand-new practice-adjacent org; rubric accepts.
- **Query / rank signals:** q2; unassigned; `bug`; 0 comments.

### 4. [CrossGL/crosstl#2799](https://github.com/CrossGL/crosstl/issues/2799)

Mojo input: kernel pointer parameters and global_idx are copied into CrossGL unchanged

- **From:** q2. 0 comments, no assignee, updated 2026-10-24. 1465 stars, release v3.4.0 on 2026-10-23.
- **Work:** lower `UnsafePointer[T, Origin]` kernel params and `global_idx` in the Mojo importer; named repro on `main` at 104868a5. Label `area:frontend` is the compiler front-end, not a web UI.
- **Fit:** healthiest repo of the five, but GPU/Mojo importer work sits outside the RAG / FastAPI / pytest preference.
- **Query / rank signals:** q2; unassigned; `bug`; 0 comments. Timeline cross-refs PRs #3059/#3076; those PRs do not close #2799.

## Rejected

| Issue | What sank it |
|---|---|
| [repowise-dev/repowise#4608](https://github.com/repowise-dev/repowise/issues/4608) | `not-actively-claimed` fail — open PR #4625 (`fix(analysis): track brace depth in C# interpolated strings during masking`) |

`not-archived`, `recent-default-branch-activity`, `repo-still-shipping`, `scope-is-one-shippable-change`, and `ai-contribution-allowed` passed for all five. `newcomer-signposted` passed on `help wanted` for all five.

```json
[
  {
    "item": "https://github.com/koda-ai-studio/agent-bom/issues/5956",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no (gh repo view isArchived=false)"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-25 commits by msaad00 on default branch, within 180 days"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "latest release v0.110.0 on 2026-10-22; last push 2026-10-25"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "one function _normalize_ocsf_event dropping actor/session/cloud/device; named fixtures; size M, still one PR"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; no comments; no open PR that references #5956"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "AGENTS.md is agent instructions for Claude/Codex/Cursor; CONTRIBUTING.md has no AI ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/DepressionCenter/Yawnalyzer/issues/14",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-09-02 commit by gabrielmongefranco (human README), within 180 days of 2026-10-25"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "releases none published; last push 2026-09-02 within 180 days, push clause carries it"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "one else branch reuses quest_name; named NameError; suggested test row"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; comments none; no linked PRs"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "no CONTRIBUTING.md / AI_POLICY.md / AGENTS.md; silence passes"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/hayagrivai-labs/phantom/issues/82",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-24 human PR merges by namanraii / bfs2021 / bh-official / alok-108"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v0.1.1 on 2026-10-21; last push 2026-10-24"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "verify inherits real stdin in execute_host_program; named files and pytest acceptance"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; comments none; issue says comment /take to claim; nobody has"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI ban; LLM generator is a product feature, not a contribution wall"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/CrossGL/crosstl/issues/2799",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-25 commits by ninglinLiu merging human PRs (#3015, #2890, #2998)"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v3.4.0 on 2026-10-23; last push 2026-10-25"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "one Mojo-importer lowering (UnsafePointer params + global_idx) with a named repro; not an umbrella"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; no claim comments; PRs #3059/#3076 are timeline cross-refs that do not close #2799"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md setup/test/PR guide; no AI ban; silence on AI passes"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/repowise-dev/repowise/issues/4608",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-25 commits by RaghavChamadiya and Aschenbath"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v0.58.0 on 2026-10-20; last push 2026-10-25"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "one C# interpolated-string hole in mask_comments_and_strings; named repro"},
      {"name": "not-actively-claimed", "grade": "fail", "evidence": "open linked PR #4625 tracks brace depth in C# interpolated strings during masking"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": ".github/CONTRIBUTING.md; 'No LLM, no spend' is a CLI flag on repowise init, not a contribution ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "reject"
  }
]
```

# Direct grades

Hand-fed URLs from the same survivor list, chosen for the pytest / ingestion sentences in the fit profile (not in the top 5 because they had more comments or sat behind 0-comment rows). **0 accepted, 2 rejected, both on `not-actively-claimed`.**

## Rejected

| Issue | What sank it |
|---|---|
| [ros2/launch#1047](https://github.com/ros2/launch/issues/1047) | `not-actively-claimed` fail — open PR #1048 (`Fix launch_testing pytest collection ignore behavior`). Pytest plugin bug, closest pytest hit on the list. |
| [docling-project/docling-pipelines#385](https://github.com/docling-project/docling-pipelines/issues/385) | `not-actively-claimed` fail — open PRs #414 and #387. Ingestion-pipeline API `total` vs `count` bug. |

```json
[
  {
    "item": "https://github.com/ros2/launch/issues/1047",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-23 commit Allow prefix blocks... (#1050) by clalancette merging a human PR"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "releases none published; last push 2026-10-24 within 180 days"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "pytest_ignore_collect returning False; one plugin hook; named repro with --ignore"},
      {"name": "not-actively-claimed", "grade": "fail", "evidence": "open PR #1048 Fix launch_testing pytest collection ignore behavior; also open #991 backport"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI/LLM statement; silence passes"},
      {"name": "newcomer-signposted", "grade": "fail", "evidence": "labels: bug only; opener anfemosa is not OWNER/MEMBER/COLLABORATOR on the issue"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/docling-project/docling-pipelines/issues/385",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-23 human commits by it-rec, pmadugundu, nsbayas (dependabot also present; human commits carry the check)"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v2.0.1 on 2026-10-09; last push 2026-10-25"},
      {"name": "scope-is-one-shippable-change", "grade": "pass", "evidence": "list_job_runs sets total=len(page); one API field; named spec scenario"},
      {"name": "not-actively-claimed", "grade": "fail", "evidence": "open PRs #414 (fix total) and #387 (tests) both reference #385"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "AGENTS.md is agent routing; CONTRIBUTING.md has no AI ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include good first issue and help wanted"}
    ],
    "verdict": "reject"
  }
]
```

# Direct grades, 2026-10-25 (unit 6, after `scope-feasible`)

Same four accepts from last week's scan, re-graded on current GitHub. All four still `accept`. Difficulty notes are live-only and not in the JSON.

## Accepted (fit order)

### 1. [koda-ai-studio/agent-bom#5956](https://github.com/koda-ai-studio/agent-bom/issues/5956) — **moderate**

`_normalize_ocsf_event` still hard-codes `agent_name=""` and `session_id=""` in `src/agent_bom/api/observability_events.py` (lines 145–146 on current main). Location is named; several fields and two OCSF class fixtures remain. Unclaimed. **Chose this one.**

### 2. [DepressionCenter/Yawnalyzer#14](https://github.com/DepressionCenter/Yawnalyzer/issues/14) — **straightforward**

Named file and loop, suggested test row. 2 stars. Unclaimed.

### 3. [hayagrivai-labs/phantom#82](https://github.com/hayagrivai-labs/phantom/issues/82) — **moderate**

Two files (`equivalence.py`, `host.py`) plus a `--stdin` design choice. Repo is four days old. Unclaimed.

### 4. [CrossGL/crosstl#2799](https://github.com/CrossGL/crosstl/issues/2799) — **ambitious**

One importer lowering, but the edge is the unfamiliar Mojo/MAX `global_idx` mapping. Unclaimed.

```json
[
  {
    "item": "https://github.com/koda-ai-studio/agent-bom/issues/5956",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-25 human commits by msaad00 on default branch"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v0.110.0 on 2026-10-22; last push 2026-10-25"},
      {"name": "scope-feasible", "grade": "pass", "evidence": "one identifiable task: map actor/session/cloud/device in _normalize_ocsf_event; open fixture edge is a difficulty note"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; comments none; no open PR referencing #5956"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md: coding agents allowed; you are responsible for every line; AGENTS.md is agent instructions not a ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/DepressionCenter/Yawnalyzer/issues/14",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-09-02 human README commit by gabrielmongefranco"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "releases none published; last push 2026-09-02 within 180 days"},
      {"name": "scope-feasible", "grade": "pass", "evidence": "one parser else-branch; named file and test row"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; comments none; no linked PRs"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "no CONTRIBUTING.md / AI_POLICY.md / AGENTS.md; silence passes"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/hayagrivai-labs/phantom/issues/82",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-24 human PR merges"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v0.1.1 on 2026-10-21; last push 2026-10-24"},
      {"name": "scope-feasible", "grade": "pass", "evidence": "one verify stdin-sharing bug; --stdin flag is an open edge, not an umbrella"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; comments none; /take not used"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI ban"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/CrossGL/crosstl/issues/2799",
    "checks": [
      {"name": "not-archived", "grade": "pass", "evidence": "archived: no"},
      {"name": "recent-default-branch-activity", "grade": "pass", "evidence": "2026-10-25 ninglinLiu merging human PRs"},
      {"name": "repo-still-shipping", "grade": "pass", "evidence": "release v3.4.0 on 2026-10-23; last push 2026-10-25"},
      {"name": "scope-feasible", "grade": "pass", "evidence": "one Mojo-importer lowering with a named repro; unfamiliar global_idx mapping is the difficulty note"},
      {"name": "not-actively-claimed", "grade": "pass", "evidence": "assignees none; PRs #3059/#3076 do not close #2799"},
      {"name": "ai-contribution-allowed", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI ban; silence passes"},
      {"name": "newcomer-signposted", "grade": "pass", "evidence": "labels include help wanted"}
    ],
    "verdict": "accept"
  }
]
```

