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

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
Scope check: codepath/pathreview-ai301-fa26-s3 is the repo named in scope.md, so the candidate is in field. Path Review house rule (classmate claim comments don't block) is noted but doesn't bite here — the thread is empty.

Check-by-check read-out (measured against today, 2026-09-23):

- Maintainer activity — pass. Last 5 default-branch commits are all by non-bot Aburke225; the newest, chore: track five more manifest entries against the tracker, landed 2026-09-16, 7 days ago — inside the 60-day bar. (The response-latency prong is thin — most recent issues have 0 comments — but the rule is an OR and the commit prong carries it.)
- Repo is in use — pass. pushedAt: 2026-09-16T21:50:20Z is 7 days ago, inside 40 days; isArchived: false.
- Newcomer-friendly scope — pass. One concrete outcome in one named file: api/routes/health.py executes the literal "SELECT 1", which SQLAlchemy 2.x requires wrapped in text(). I confirmed the line is really there — health.py:32: await db.execute("SELECT 1"). Not an umbrella issue, not a support question, outcome not in debate. Labeled good first issue and tier-1.
- Nobody actively working on it — pass. assignees: [], 0 comments, and the timeline holds only four labeling events from the minute it was opened — no assignment, no cross-reference. The repo has zero pull requests in any state, so there is no linked PR and no history of abandoned attempts.
- AI contribution policy — pass. No CONTRIBUTING.md at root or in .github/; the real one is docs/CONTRIBUTING.md, and a grep for AI/LLM/Copilot/generated/disclosure language returns no policy text (only incidental substring hits like "main"). The PR template asks for testing and CI, not an AI disclosure. Silence passes.

Fit note (ranking only, does not move the verdict): this is a strong match for your profile — a Python FastAPI/SQLAlchemy backend fix, squarely the backend work you said you want over frontend, and small enough to be a real first contribution. One practical heads-up from docs/CONTRIBUTING.md: seeded bugs carry a @pytest.mark.xfail(strict=True) marker, and removing that marker is part of the fix or CI will fail.

All five required checks pass.

{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61",
  "checks": [
    {"name": "Maintainer activity", "grade": "pass",
     "evidence": "Newest default-branch commit 2026-09-16 by non-bot Aburke225 ('chore: track five more manifest entries against the tracker'), 7 days before today — within 60 days."},
    {"name": "Repo is in use", "grade": "pass",
     "evidence": "pushedAt 2026-09-16T21:50:20Z (7 days ago, within 40) and isArchived: false."},
    {"name": "Newcomer-friendly scope", "grade": "pass",
     "evidence": "Concrete single-file fix: api/routes/health.py:32 is `await db.execute(\"SELECT 1\")`, needing sqlalchemy.text(); labeled 'good first issue' and 'tier-1'."},
    {"name": "Nobody actively working on it", "grade": "pass",
     "evidence": "assignees: [], 0 comments, timeline has only 4 labeling events from 2026-09-10, and the repo has zero PRs in any state."},
    {"name": "AI contribution policy", "grade": "pass",
     "evidence": "docs/CONTRIBUTING.md contains no AI/LLM/generated-code policy and the PR template requires only testing and CI — silence, no ban."}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history** 
agreement: 17/20 scored items  (bar: 18/20: below the bar)
agreement: 1/3 scored items
agreement: 16/20 scored items  (bar: 18/20: below the bar)
agreement: 1/5 scored items
agreement: 5/5 scored items
agreement: 19/20 scored items  (bar: 18/20: PASS)
agreement: 19/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

issue-20

Rubric decision: reject
Gold label: reject

Failed check: Newcomer-friendly scope

"evidence": "Issue requests a brand-new toolbar shape type integrated across placement/resize/move/export like other elements, with surface only 'likely'/'possibly' and 'Logo asset TBD' — broad core-internals change with no concrete, decided target."

**Check rationale**

"Newcomer-friendly scope | Issue body and comment thread | The issue has a clear, bounded outcome and enough direction for a newcomer to know what to change. Touching multiple files or having detailed requirements does not fail this check by itself. Reject tracking issues, unresolved design discussions with no settled direction, support questions, or work that requires changing core internals. | required"

I changed this check because my earlier version was too strict about the size of an issue. It was rejecting issues just because they touched multiple files or had detailed requirements, even when the actual goal was clear and manageable. I changed it to focus more on whether a newcomer can understand what needs to be done and whether the outcome is clearly defined.

**Trade-offs**

A trade-off with this check is that making the scope rule less strict can allow some issues that look bounded at first but may actually be more complicated. I re-ran issue-20 as a canary, and the final result was:

issue-20  reject  reject   yes

It failed the Newcomer-friendly scope check because the issue required a new toolbar shape across placement, resize, move, and export, while parts of the implementation were still undecided.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. This issue fits my interests because I want to get better at backend development, and it involves Python, FastAPI, and SQLAlchemy. It also seems small enough for me to work through as my first open-source contribution without taking too much time.

2. The verdict correctly identified that the issue has a clear and specific fix, the repository is active, and nobody is currently working on it. The rubric could tell me whether the issue was suitable, but it could not really account for my personal interest in backend development or the fact that I want to get more comfortable debugging Python projects, so I considered those things when choosing it.

3. I don't expect claiming it to be too difficult because there is no assignee or open pull request for the issue. The part that may be difficult for me is that this is my first time contributing to an open-source project, so I am still learning how the claiming and contribution process works.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
