# Procedure: how this skill grades a plan package

## Read order

1. Determine whether the input is an eval bundle or a live package.
   In eval mode, use only the bundle and ignore scope and voice files.
   In live mode, read scope.md first; stop without grading if the repo
   placeholder remains or the issue is outside scope. Read voice-guide.md.
2. Read rubric.md and references/evidence-guide.md. Identify every
   check, its pass condition, evidence location, and weight.
3. Read the issue, repository facts or applicable docs, and thread.
   Record the requested behavior and explicit contributor constraints.
4. Read reproduction evidence before the candidate plan. Record the
   failing steps, actual and expected results, and controls. This keeps
   the candidate's explanation from replacing the observed facts.
5. Read the whole candidate plan, then the candidate comment. Record
   diagnosis, changes, boundaries, implementation steps, tests,
   uncertainties, and factual claims. Do not grade until both are read.

## Evidence gathering

1. For grounded-diagnosis, pair each causal claim in the plan and
   comment with reproduction results and controls. Record support,
   contradictions, and any concrete verification of a hypothesis.
2. For cause-directed-change, connect each proposed intervention to
   the supported mechanism. Record whether it resolves that mechanism
   or merely suppresses the symptom.
3. For bounded-scope, list proposed changes and their purpose. Compare
   them with the issue outcome and maintainer constraints; flag unrelated
   features, rewrites, or changes beyond the stated boundaries.
4. For executable-approach, record the starting file or component,
   intended operation, necessary sequence, and specific investigation
   steps for unresolved decisions.
5. For decisive-tests, pair proposed test actions and assertions with
   the reproduced failure. Record the expected changed outcome and
   relevant controls or neighboring behavior.
6. For honest-claims, list consequential claims about completed work,
   certainty, approval, and assumptions. Check them against supplied
   evidence; record material unknowns and their resolution steps.
   If deviations are included, record what changed and why.
7. For thread-and-policy, extract each applicable explicit maintainer
   request and contribution or AI-policy requirement. Compare the
   comment with each requirement and with its own plan.
8. Use the evidence-guide locations for each family. In live mode,
   gather issue and repo evidence as described there. Do not substitute
   unquoted local files for missing house reproduction evidence.
   Record source locations with facts so grades can be traced.

## Check execution

1. Execute all checks in rubric table order. Do not stop at the first
   failure and do not use an expected or gold verdict to guide grading.
2. For each check, compare the gathered facts with its exact pass
   condition. Assign pass when that condition is established, fail
   when evidence contradicts it or required content is absent, and
   unclear when unavailable or ambiguous evidence prevents a decision.
3. Before marking content absent, reread the relevant plan and comment
   passages and follow explicit references within the allowed evidence.
   Required content may appear anywhere; headings and length do not
   determine readiness. Do not invent missing implementation or tests.
4. Use recorded evidence without rereading the whole package unless
   a conflict or ambiguity requires returning to the relevant source.
   Grade related checks independently against their own conditions.
5. Do not require exact code, line numbers, automated tests, dedicated
   scope or risks sections, or disclosures not required by policy.
   Do not mistake limited review capacity for a ban on contributions.
6. In live mode, also compare the comment with voice-guide.md and
   quote broken personal rules in the readable summary. Keep that
   feedback separate from rubric grades unless a rubric condition
   independently fails.

## Verdict assembly

1. Include a result for every rubric check.
2. Apply the rubric's verdict rule: accept only if all required checks
   pass; reject if any required check fails or is unclear. Preferred
   checks do not change the verdict.
3. For each check, provide a short quote or precise fact and its source
   location. For missing evidence, name exactly what was absent or
   inaccessible. For rejection, identify all deciding required checks
   in the readable summary.
4. Report any procedure gap rather than inventing a grading step.
5. Finish with a valid fenced JSON block containing item, checks, and
   verdict. Each check contains name, grade, and evidence. Use the
   exact rubric check names and pass, fail, or unclear grades.
   Use the bundle id in eval mode and issue URL in live mode.
   Put nothing after the JSON block.
