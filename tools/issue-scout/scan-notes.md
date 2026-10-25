# Scan notes

2026-10-25. First query pass: `gh search issues --label "good first issue" --language python --state open --limit 100` returned 100 hits, and the first result was already `authorAssociation: OWNER` with `createdAt` today. The original Q3 string `RAG OR FastAPI OR ingestion OR pytest OR embedding` with `good first issue` returned `[]`. Ranking with drop-assignee + drop-OWNER + fewest comments then filled the shortlist with 0-comment org issues updated today (moodsona persona cards, a class NMT repo). Qiskit/qiskit#17316 was the one real project in that first five.

Patched `search-strategy.md`: rewrite Q3 to `--label bug --language python pytest` (the empty OR query was not a query), and drop results whose labels do not include `bug`. Re-ran. Combined 298 unique issues; dropped 149 OWNER, 43 assigned, 27 non-bug, 4 frontend/ci, 4 stale; 71 survivors. New top 5 are all `bug`+`help wanted` with 0 comments.

Graded those five against the Unit 1 rubric (no stars check added). Four accept, one reject (`not-actively-claimed` on repowise#4608, open PR #4625). Yawnalyzer is 2 stars and phantom is 4 stars and four days old; both still accept because `recent-default-branch-activity` and `repo-still-shipping` pass on any recent human push, and a required 100-star floor would reject gold `issue-06` (Itqan-community/quran-apps-directory, 37 stars, clear-accept). Left the rubric alone. Fit among the accepts is agent-bom (API ingest), then Yawnalyzer / phantom (named tests), then crosstl (healthy Python repo, Mojo importer, outside the preferred areas).

`area:frontend` on CrossGL/crosstl#2799 is the compiler front-end, not a React UI. Exact label match in the ranking filter kept it, which is what I want. Linked-PR false positives showed up on the CrossGL timeline (PRs #3059/#3076 do not close #2799); `not-actively-claimed` still needs the Development closing-ref / claim-comment read, not the raw timeline.

Nothing else in `rubric.md` mis-graded a required check on this scan. Next week: Candidate Issues site picks get a direct grade; claim on GitHub only after that.
