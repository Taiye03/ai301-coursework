# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**Where it lives**

- In Eval mode, read the plan-context block for the planned scope, boundary, implementation steps, test plan, and any recorded deviations. Read the candidate PR's unified diff for the files and behavior actually changed, and read factual implementation claims in the candidate PR description.
- In Live mode, read `plan.md`, including any `## Deviations`, and compare it with the branch diff from `git diff main...HEAD`. Read implementation claims in the title and description from `pr_draft.md` against that same diff.

**What good looks like**

Every material change in the diff falls within the plan's stated boundary or is accounted for by an honest deviation note, and material planned work is either implemented or its omission is disclosed. Claims in the PR description agree with what the diff actually contains. Silent drift exists when the branch materially does more or less than the plan without disclosure, or when the description claims implementation that the diff contradicts.

## Test evidence (harness category: not-tested)

**Where it lives**

- In Eval mode, read the package's test-evidence section together with the plan-context test plan, reproduction evidence, changed behavior in the diff, and any repository checks named in the repo-facts block.
- In Live mode, read `test_evidence.md` together with the test plan in `plan.md`, the relevant changed behavior in `git diff main...HEAD`, and the repository's stated test or validation requirements.

**What good looks like**

The evidence identifies an observable behavior or command, the expected or relevant outcome, and the actual result. It covers testing relevant to the changed behavior and records the outcomes of repository checks that were actually run. A failure or unavailable check may be acceptable when it is explicitly and accurately disclosed; a bare statement such as "tests pass" without observable supporting evidence is not decisive proof.

## Diff quality (harness category: unreviewable)

**Where it lives**

- In Eval mode, inspect the candidate PR's unified diff and commit information supplied in the bundle.
- In Live mode, inspect the complete `git diff main...HEAD` and the branch's commits when needed to understand what is being submitted.

**What good looks like**

The intended change is visible and reviewable without material unrelated work obscuring it. Look for accidental files, unrelated hunks, debug output, dead or commented-out code, generated debris, broad formatting churn, or drive-by edits. Size alone does not make a diff unreviewable; the deciding question is whether unrelated or accidental changes materially interfere with reviewing the intended change.

## Standards and comms (harness category: standards-wall)

**Where it lives**

- In Eval mode, read the repo-facts block for PR-template asks, contribution instructions, stated policy, required issue linkage, disclosure requirements, and any explicit maintainer direction. Compare those requirements with the candidate PR title and description.
- In Live mode, read the repository PR template, `docs/CONTRIBUTING.md`, relevant explicit maintainer direction in the issue thread, and the title and description in `pr_draft.md`.

**What good looks like**

The draft satisfies the repository's substantive submission requirements with real, truthful content: required issue linkage is present, testing and limitations are disclosed accurately, required template information is addressed, and required AI-use or other disclosures are included. Boilerplate that does not answer a substantive ask, or silently ignoring an explicit repository requirement, is evidence of a standards wall. Whether implementation claims match the actual diff is graded under Plan fidelity rather than duplicated here.