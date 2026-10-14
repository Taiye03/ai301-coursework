# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Plan fidelity | The branch diff from `git diff main...HEAD` read against the scope, implementation steps, and any `## Deviations` recorded in `plan.md`; also compare factual implementation claims in the PR description with the diff. | Pass when the diff implements work within the plan's stated scope or honestly recorded deviations, and the PR description does not materially misrepresent what the diff actually changes. Fail when the diff contains material unrecorded drift, omits planned work without disclosure, or the description claims implementation fidelity contradicted by the diff. | required |
| Test evidence | `test_evidence.md` read against the plan's test plan, the changed behavior visible in the diff, and the repository's stated checks. | Pass when the evidence shows observable testing relevant to the changed behavior and records the repository checks that were actually run, with outcomes stated honestly. A disclosed failure or unavailable check may still pass this check when the evidence makes the shortfall explicit rather than claiming success. Fail when testing is absent, irrelevant to the change, unverifiable, or required checks are silently omitted. | required |
| Diff quality | The files and hunks in `git diff main...HEAD`, read against the issue and the plan's intended boundary. | Pass when the diff is focused enough for a reviewer to identify and evaluate the intended change, with no material unrelated changes, generated debris, debugging leftovers, or accidental files obscuring the work. Fail when unrelated or accidental changes materially interfere with review. | required |
| Standards and comms | The draft title and description in `pr_draft.md` read against the repository PR template, `docs/CONTRIBUTING.md`, issue linkage, the diff, and any required AI-use disclosure. | Pass when the draft communicates the actual change and testing truthfully, satisfies the repository's substantive template and contribution-policy asks, links or identifies the issue as required, and includes required disclosure. An honestly disclosed limitation does not fail merely because the work is imperfect. Fail when a substantive repository requirement, issue linkage, or required disclosure is ignored or materially misrepresented. | required |

## Verdict rule

Return `accept` only when every required check is `pass`.

Return `reject` when any required check is `fail` or `unclear`. Treat `unclear` as failing because evidence that cannot be verified from the available package is not sufficient to declare the pull request ready to submit.

Preferred checks, if any are added later, may be reported but never change the final verdict.