---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Grade exactly one PR package to answer one question: is this pull request ready to submit?

Treat the PR package as the candidate PR title and description, the committed branch diff, test evidence, and the plan the change claims to implement, read against the issue and the repository's stated contribution requirements. Do not grade unrelated work or substitute general impressions for the checks defined by this skill.

## Inputs and modes

Use exactly one of these modes:

- **Live mode**: read the student's `plan.md`, including any `## Deviations` notes; the committed branch diff produced by `git diff main...HEAD` from the working copy; the draft PR title and description in `pr_draft.md`; the test evidence in `test_evidence.md`; and the issue identified by the URL in the request. Gather issue-side evidence from the real repository, including the issue thread, repository PR template, and `docs/CONTRIBUTING.md`. Read the diff as the complete set of committed changes the branch makes relative to `main`. For a house-chain student, use the house plan and house repro pack instead of the student's own plan and reproduction evidence while applying the same checks.
- **Eval mode**: read only the supplied package bundle. Treat the bundle as the whole world. Do not fetch anything, inspect other files, or use outside repository knowledge. Run every rubric check and apply the complete verdict rule using only evidence contained in the bundle.

Do not mix evidence between modes.

## The scope seam (live mode only)

In live mode, read `scope.md` before gathering or grading any other evidence. Apply the repository and house rules it defines.

Refuse to grade if the requested work is outside the repository named by the `Repo:` line. If that line still contains an unfilled placeholder, stop without grading and tell the student to fill the `Repo:` line with their section's Path Review repository. Never guess the intended repository.

In eval mode, ignore `scope.md` completely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and check both the draft PR title and description against its writing rules. If either breaks a rule, report the broken rule and relevant draft text in the readable summary.

Voice-guide findings do not change the final verdict by themselves unless a check in `rubric.md` explicitly makes that evidence part of its pass condition.

In eval mode, ignore `voice-guide.md` completely.

## Component reads

Read `rubric.md` for the checks, their evidence requirements, pass conditions, weights, and final verdict rule.

Use `references/evidence-guide.md` to locate each evidence family in the PR package and determine what usable evidence looks like in live and eval modes.

Execute `procedure.md` exactly as written for read order, evidence gathering, check execution, and verdict assembly. Do not invent a missing procedure step. If the procedure is silent about a needed step, report that gap rather than improvising around it.

If `rubric.md` contains no substantive checks or `procedure.md` contains no substantive operating steps, stop and refuse to grade. Do not invent checks or a workflow at runtime.

## Verdict and output

Use only two final verdicts: `accept` means the PR is ready to submit, and `reject` means the PR should be held.

Grade every rubric check as `pass`, `fail`, or `unclear` and include one evidence line identifying the fact or quote that determined the grade. Apply the verdict rule from `rubric.md`.

A short readable per-check summary may appear before the JSON. End every completed grading response with the following fenced JSON block. It must be valid, must use this schema exactly, and nothing may appear after it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Grade evidence first. Never assign a check grade without identifying the concrete fact or quote that determines it. "Looks fine" is not evidence.
- Grade the actual PR package, not its polish or confidence. Compare the diff, plan, tests, description, issue, and repository standards where the rubric requires them.
- Let `rubric.md` decide the grades and verdict. If evidence satisfies a written pass condition, apply that condition even if it feels wrong; the rubric must be revised instead of changing the rule during a run.
- Let `procedure.md` decide how grading is performed. Follow its steps as written and report gaps instead of improvising.
- Treat unverifiable evidence as `unclear`. Apply the rubric's verdict rule to unclear grades. If the rule is silent, treat `unclear` as failing because an unverifiable PR is not ready to submit.