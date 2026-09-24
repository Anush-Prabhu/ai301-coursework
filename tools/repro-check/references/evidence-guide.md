# Evidence guide: where proof lives in a reproduction package

The rubric names the checks. This file is the map: where each kind of
proof sits in an eval package or on a live issue, and what good looks
like there.

## Environment

**Where it lives (eval):** the environment line(s) at the top of the
Candidate repro report. Cross-check any version named in the Issue
section or the repo-facts `latest release` line.

**Where it lives (live):** the draft repro comment's environment block;
confirm against `gh` for the commit/branch you actually ran, and the
issue body's version claims if any.

**What good looks like:** OS + under-test version pinned to something a
stranger can check out again (tag, SHA, or branch@date) + dependency
versions only when the failing path goes through them. "Latest" alone
fails.

## Steps

**Where it lives (eval / live):** the Steps section of the Candidate
repro report (or draft comment).

**What good looks like:** a stranger with only the public repo can reach
the same state. Commands are written as run. Fixtures are inlined or
linked publicly. Fails when a private monorepo, unshared config, or
"my usual setup" is required.

## Behavior shown

**Where it lives:** the pasted artifact inside the repro report —
traceback, stdout/stderr, listing, measurement — read against the Issue
section's described behavior.

**What good looks like:** issue subject and artifact subject are the
same. Adjacent errors, wrong versions, self-inflicted edits, and
"proof of life" banners fail this family.

## Honesty

**Where it lives:** the report's Expected / Actual / conclusion lines,
compared to the artifact just above them.

**What good looks like:** reproduced-with-artifact passes; cannot-
reproduce-with-a-real-attempt passes; confident diagnosis or
"guaranteed" with no artifact fails.

## Comms

**Where it lives (eval):** Candidate claim comment + contribution-
policy line in repo facts. **Live:** draft claim/repro comments +
`docs/CONTRIBUTING.md` (and any AI policy the repo links).

**What good looks like:** claim names this issue's specific behavior
and a concrete next step; no assign-me boilerplate; no date promises.
If the policy requires AI disclosure, the comment discloses. Silence
in the policy asks for nothing extra.
