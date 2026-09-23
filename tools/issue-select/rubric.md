# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer activity | Last 5 default-branch commits and maintainer first-response sample under Repo facts | At least one non-bot commit was made within 60 days OR maintainers respond to issues within 7 days | required |
| Repo is in use | "last push to any branch" and "archived:" under Repo facts | The repo has had a push within the last 40 days and is not archived | required |
| Newcomer-friendly scope | Issue body and comment thread | Pass when the issue describes a concrete outcome or change to implement. A short issue, multiple files, multiple substeps, optional suggestions, or multiple possible causes do not fail this check by themselves. Reject only if it is a tracking/umbrella issue, a usage/support question, the requested outcome itself is still undecided, or the issue explicitly requires broad changes to core internals without a concrete target. | required |
| Nobody actively working on it | Assignees, linked PRs, and dated claim comments in the Comments section | Pass if there is no current assignee, open linked PR, or recent evidence that someone is actively working on the issue. A single old or abandoned attempt does not fail this check. Reject if the history shows several separate abandoned implementation attempts or closed unmerged PRs, because repeated failed attempts are evidence that the issue may be unsuitable for a first contribution. | required |
| AI contribution policy | Contribution policy under Repo facts, including CONTRIBUTING.md or any AI policy | The repo does not ban AI-assisted contributions; requirements to disclose, understand, review, or test AI-assisted work are okay | required |

## Verdict rule

Accept the issue if all required checks pass. Reject it if any required check fails. If a required check is unclear, treat it as a fail.
