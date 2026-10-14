# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**
https://github.com/codepath/pathreview-ai301-fa26-s3/pull/222

**Branch**
fix/61-health-probe-text

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**
20/20, 20/20

**Package analysis**

pkg-03 — My rubric decided `reject`, and the gold label was `reject`. This package was categorized as `silent-drift`. The rubric rejected it because the Plan fidelity check requires the branch diff to stay within the plan's stated scope or have deviations honestly recorded. Material unrecorded drift therefore fails the check and makes the PR not ready to submit.

**Check rationale**

"Plan fidelity | The branch diff from `git diff main...HEAD` read against the scope, implementation steps, and any `## Deviations` recorded in `plan.md`; also compare factual implementation claims in the PR description with the diff. | Pass when the diff implements work within the plan's stated scope or honestly recorded deviations, and the PR description does not materially misrepresent what the diff actually changes. Fail when the diff contains material unrecorded drift, omits planned work without disclosure, or the description claims implementation fidelity contradicted by the diff. | required"

I made this check explicit so implementation changes are judged against both the original plan and recorded deviations rather than requiring exact adherence to the original plan. This allows legitimate changes when they are disclosed while still rejecting silent scope drift.

**Trade-offs**

This check gives up strict plan adherence in favor of allowing honestly documented deviations. A PR can still pass Plan fidelity when its implementation differs from the original plan, as long as the deviation is recorded and the PR description truthfully represents the resulting change. The final eval still scored 20/20, including all four `silent-drift` packages, so this trade-off did not cause those cases to be incorrectly accepted.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
