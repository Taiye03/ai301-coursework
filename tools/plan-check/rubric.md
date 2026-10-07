# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| grounded-diagnosis | Candidate plan's diagnosis and candidate comment's causal claims, compared with the repro evidence's steps, results, and controls. | The explanation accounts for the observed failure and relevant controls without contradicting them. A proposed cause may remain a hypothesis if clearly identified and paired with a concrete verification step. A thread claim alone cannot override contrary reproduction evidence. | required |
| cause-directed-change | Candidate plan's proposed changes compared with its diagnosis and the repro evidence. | The proposed change addresses the supported failure mechanism rather than hiding the symptom, suppressing the error, or changing the expected behavior without justification. | required |
| bounded-scope | Candidate plan's included work, exclusions, affected files or areas, compared with the issue and maintainer constraints. | The work forms one focused fix or explicitly proposed behavior change. Each included change is necessary to implement, test, or document that outcome; unrelated rewrites and features are excluded. An explicit out-of-scope heading is not necessary if the boundaries are otherwise clear. | required |
| executable-approach | Candidate plan's implementation steps, named files or components, and approach, compared with repo facts and reproduction details. | Another contributor can identify where to begin and what concrete change or investigation to perform. Critical implementation decisions are described, or unresolved decisions have specific investigation steps. “Look around and fix it” is insufficient; exact line numbers and complete code are unnecessary. | required |
| decisive-tests | Candidate plan's test actions and expected results, compared with the repro evidence's failing case and relevant controls. | Tests directly exercise the reported failure and specify an observable result that distinguishes the broken behavior from the intended behavior. Relevant controls or affected neighboring behavior are checked when needed. Manual tests and explicit references to reproduction steps are valid. Running an existing suite alone is insufficient unless a named existing test demonstrably covers the failure. | required |
| honest-claims | Candidate plan and comment's verification claims, assumptions, risks, unknowns, and any deviation notes, compared with repro evidence and repo facts. | Claims do not invent completed investigation, tests, approval, or certainty unsupported by the package. Material uncertainties are acknowledged with a way to resolve them; recorded deviations explain what changed and why. Do not require a risks section or penalize ordinary future-tense intentions by themselves. | required |
| thread-and-policy | Candidate plan comment compared with issue thread highlights, applicable repo conventions, contribution policy, and any AI-use requirements. | The comment accurately communicates its own proposed approach and respects explicit maintainer requests and applicable contribution requirements. Required disclosures are included when applicable. It does not contradict the plan or imply approval that was never given. Limited review capacity is not a contribution ban, and lack of an AI policy does not create a disclosure requirement. Bug-report template fields need not be repeated in a plan comment unless requested there. | required |

## Verdict rule

Return accept only when every required check passes.
Return reject when any required check fails or is unclear.
Preferred checks, if added later, never change the verdict.

Grade every check and cite the specific evidence or missing information
that determines its result. Judge substance rather than length, headings,
tone preferences, or formatting.
