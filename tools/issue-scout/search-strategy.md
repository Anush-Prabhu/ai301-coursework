# Search strategy: where your scout looks, and why

<!--
THIS IS THE PART YOU WRITE. The scout in SKILL.md executes whatever
queries and filters you define here. It ships empty on purpose: the
strategy is your judgment about where YOUR first contribution lives,
and a scan without authored queries is just someone else's defaults.

A filled strategy must contain:

1. At least one query in the Queries section. Each query is a real
   `gh search issues` invocation, and each should trace to a sentence
   of your fit profile in scope.md: if you cannot say which sentence
   produced a query, the query is probably not yours. Search breadth
   is the point at this stage: prefer generous limits and let the
   ranking filters do the narrowing.

2. At least one ranking filter in the Ranking filters section. A
   filter is a condition or an ordering over fields the search
   results already carry (last activity date, assignee presence,
   label set, comment count, repo). It must be checkable from the
   result fields alone: if deciding it would need opening the issue
   page, it belongs in your rubric, not here. Ranking is the free
   stage; keep it free. Make at least one filter an ordering, or
   state your tie-break: with drop conditions alone, the scout takes
   the top of whatever order the searches happened to return, and
   the graded candidates stop being traceable to you.

3. The top-N line, kept or deliberately changed.
-->

## Queries

Each query is a real `gh search issues` line. The comment above it is
the fit-profile sentence it came from. `--state open` and `--limit 100`
are on every query so closed issues never mix in and GitHub does not
stop at 30.

# I am comfortable in Python (FastAPI, pytest, RAG pipelines, ingestion and scoring code)
gh search issues --label "good first issue" --language python --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url,authorAssociation,createdAt

# I want a small bug with a clear failing path — preferably in retrieval, API, ingestion, safety, or tests
gh search issues --label "help wanted" --label bug --language python --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url,authorAssociation,createdAt

# I prefer issues with an existing test fixture or a named crash
gh search issues --label bug --language python --state open --limit 100 --json title,repository,labels,assignees,commentsCount,updatedAt,url,authorAssociation,createdAt pytest

## Ranking filters

Apply these in order to the combined, deduplicated results, using only
fields `gh search issues` already returned. "Today" is the scan date.

1. Combine the query lists and drop duplicates by `url`.
2. Drop any result with one or more `assignees`.
3. Drop any result whose `repository.nameWithOwner` starts with
   `codepath/` — that is the course sandbox, not the wild.
4. Drop any result whose `authorAssociation` is `OWNER`. An owner
   filing their own `good first issue` is the brand-new personal or
   practice-repo pattern the fit profile wants to avoid. Organization
   issues show `MEMBER`, `COLLABORATOR`, `CONTRIBUTOR`, or `NONE`.
5. Drop any result whose labels include, case-insensitively, any of:
   `frontend`, `react`, `javascript`, `typescript`, `css`, `ui`,
   `devops`, `ci`. (Fit profile: no frontend redesigns, no devops/CI.)
6. Drop any result whose labels do not include `bug`. The fit profile
   wants a small bug with a failing path, not a persona card or a
   docs chore that happened to carry `good first issue`.
7. Drop any result whose `updatedAt` is more than 90 days before today.
8. Order the rest by **fewest comments first**. When comment counts
   tie, keep the order the searches returned. Do not break ties by
   newest update: that fills the shortlist with issues opened in the
   last hour.
9. Walk that order and keep only the first result from each repository,
   so the five graded issues come from five different repos.
10. Take the top 5.

## How many to grade

Grade the top **5** ranked results per scan.
