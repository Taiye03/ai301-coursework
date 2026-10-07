# Evidence guide: where evidence lives in a plan package

## Evidence boundaries

In eval mode, use only the supplied bundle. Do not fetch GitHub,
inspect a local repository, or use gold labels as grading evidence.
Treat candidate claims as claims to check, not independent proof.

In live mode, read scope.md first. Read the issue body and complete
thread with gh issue view <URL> --comments or the GitHub API.
Locate the student's posted Unit 2 reproduction comment by author
and content; record its URL and relevant evidence. Read applicable
repository contribution docs, templates, and AI policy through gh
or the GitHub API. An unavailable source is unknown, not proof that
no requirement exists.

For a house issue, use the house reproduction evidence actually
quoted in the drafts. Do not fill missing evidence from other local
files. Read the supplied plan and draft comment as the package.

## Diagnosis and grounding

Checks: grounded-diagnosis, cause-directed-change.

Eval locations: Issue, Thread highlights, Repro evidence, and the
Candidate plan and Candidate plan comment's causal explanations and
proposed changes.
Live locations: issue body, relevant thread comments, student's
posted reproduction, and diagnosis and changes in the supplied drafts.

Record the failing input or action, actual and expected behavior,
controls, proposed cause, and proposed intervention.
Good evidence connects the intervention to the observed mechanism
and explains relevant controls. A thread's suggested cause does not
override a reproduction that contradicts it. A plausible hypothesis
can remain tentative with a concrete verification step.

## Scope

Check: bounded-scope.

Eval locations: Candidate plan's included changes, exclusions,
affected files or components; Issue, Thread highlights, and Repo facts.
Live locations: supplied plan's scope and changes, issue requests,
and applicable repository constraints.

Record each proposed change and its relationship to the intended fix.
Good scope includes only implementation, tests, and documentation
needed for one outcome. Multiple files can serve one bounded fix;
a single file can still contain unrelated scope creep. Exclusions
may be clear from the approach without a separate heading.

## Executability

Check: executable-approach.

Eval locations: Candidate plan's approach, implementation steps,
named files or components, read against Repo facts and Repro evidence.
Live locations: approach and steps in the supplied plan, compared
with issue evidence and relevant repository documentation.

Record the starting component, concrete operation, dependencies,
order where necessary, and any unresolved decision's investigation.
Good instructions let another contributor start without inventing
the main approach. Complete code and exact line numbers are not
required. “Investigate the code and fix it” is not enough.

## Test plan

Check: decisive-tests.

Eval locations: Candidate plan's test actions and expected outcomes,
compared with Repro evidence's steps, artifacts, and controls.
Live locations: draft test plan compared with the posted reproduction
or house evidence quoted in the drafts.

Record the failing scenario exercised, the proposed assertion or
manual observation, and relevant controls or affected behavior.
Good tests distinguish the reproduced failure from success.
Referencing reproduction steps is sufficient if the intended changed
outcome is specified. Manual checks are valid. A generic suite run
does not establish that the reported failure is covered.

## Honesty

Check: honest-claims.

Eval locations: factual claims, certainty, assumptions, risks, and
deviations in both Candidate plan and Candidate plan comment, compared
with Repro evidence, Thread highlights, and Repo facts.
Live locations: claims and deviation notes in both drafts, compared
with the posted evidence and documented thread or repo facts.

Record consequential claims of completed work, causal certainty,
approval, and unresolved assumptions with their supporting evidence.
Good plans distinguish observations from hypotheses and future work.
Material unknowns have a resolution step; changed plans explain what
changed and why. Missing a dedicated risks heading is not itself
dishonesty. Future intentions do not prove completed work.

## Comms

Check: thread-and-policy.

Eval locations: Candidate plan comment read against Candidate plan,
Thread highlights, and Repo facts' contribution and AI policies.
Live locations: draft comment, supplied plan, complete issue thread,
repository contribution docs and AI policy; voice-guide.md supplies
additional personal feedback in live mode only.

Record applicable explicit requests, policy obligations, and the
comment's response to each. Good comments state their own approach,
respect maintainer constraints, and include required disclosures.
Do not invent bans, disclosure requirements, or demands to repeat
bug-report fields in a plan comment. Limited review capacity alone
does not forbid a PR. Do not assume AI authorship from writing style;
use only supplied evidence about authorship or tool use.

In live Path Review mode, apply scope.md's house rules: classmates'
plans do not block this student's own plan, piggybacking is not a
substitute for an independent plan, and build branches belong on the
student's fork. Report personal voice-guide violations separately;
they do not independently change this rubric's verdict.
