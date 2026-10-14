# Procedure: how this tool grades a PR package

## Read order

1. Determine whether the run is Live mode or Eval mode. In Live mode, confirm that the scope requirements in `SKILL.md` have already been satisfied. In Eval mode, use only the supplied bundle.

2. Read `rubric.md` and `references/evidence-guide.md` before grading so the required checks, verdict rule, and evidence locations are known.

3. Read the issue context first. Record the requested behavior, relevant constraints, and acceptance expectations.

4. Read `plan.md` next, including any `## Deviations`. Record the intended scope, files or components expected to change, implementation approach, and planned testing. Reading the plan before the diff prevents the implementation from redefining what the plan originally promised.

5. Read the branch diff from `git diff main...HEAD`. Record the changed files and the material behavior changed by each relevant hunk. Compare these observations with the plan and its recorded deviations.

6. Read `test_evidence.md`. Record which reproduction steps, behavioral tests, and repository checks were actually run and their observed outcomes. Compare this evidence with the plan's test plan and the behavior changed by the diff.

7. Read the draft PR title and description in `pr_draft.md`. Record the implementation claims, issue linkage, testing claims, limitations, deviations, and disclosures. Compare those claims with the plan, diff, and test evidence.

8. Read the repository standards evidence: the PR template and `docs/CONTRIBUTING.md` in Live mode, or the corresponding repo-facts evidence in Eval mode. Record only substantive requirements relevant to submission.

## Evidence gathering

For **Plan fidelity**, pair the files and behavior changed in the diff with the plan's stated scope and implementation steps. Include recorded deviations when deciding the expected boundary. Also pair factual claims in the PR description with the actual diff. Record any material planned work that is absent, unplanned work that appears, or description claim contradicted by the diff.

For **Test evidence**, pair the tests and checks recorded in `test_evidence.md` with the plan's test plan and the behavior actually changed in the diff. Record the command or observable action, its result, and any honestly disclosed failure, omission, or unavailable check. Do not treat a claim that testing occurred as evidence without an observable result.

For **Diff quality**, inspect the complete diff and record unrelated hunks, accidental files, generated debris, debugging leftovers, or other changes that materially interfere with reviewing the intended work. Do not fail a focused diff merely because it is large or small.

For **Standards and comms**, compare the title and description with the repository's substantive PR-template and contribution requirements. Record whether the issue is linked as required, whether implementation and testing claims match the gathered evidence, and whether required AI-use or other disclosures are present.

## Check execution

1. Execute the rubric checks in their table order: Plan fidelity, Test evidence, Diff quality, then Standards and comms.

2. For each check, use only the evidence gathered for that check and apply its written pass condition exactly. Do not add a stricter or looser condition during the run.

3. Grade the check `pass` when the gathered evidence satisfies its pass condition. Grade it `fail` when the evidence demonstrates that the pass condition is not satisfied.

4. Grade the check `unclear` when the evidence needed to decide the written condition is genuinely missing, conflicting, or unverifiable. Do not turn missing evidence into an assumption.

5. Record one concise evidence line for every grade naming the concrete fact or quote that decided it. Once the needed evidence has been gathered, do not re-read unrelated parts of the package merely to search for a preferred outcome.

## Verdict assembly

1. Apply the verdict rule in `rubric.md` to the completed check grades.

2. Return `accept` only when every required check passes. Return `reject` when any required check is `fail` or `unclear`.

3. If the verdict is `reject`, identify the first failing or unclear required check in rubric order as the primary deciding check. If several checks fail, still report evidence for all of them, but use that first required failure as the primary reason in the readable summary.

4. If the verdict is `accept`, state that all required checks passed.

5. Produce the per-check results and evidence lines, then emit the exact JSON schema required by `SKILL.md`. The JSON block must be valid and must be the final content in the response, with nothing after it.