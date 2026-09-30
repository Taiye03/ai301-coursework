# Rubric: is this reproduction package ready to post?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment | The repro report's environment record, read against the issue environment and repo-facts requirements. | Pass when the report identifies enough relevant version, platform, installation/build, or other environment details to tell what was actually tested and to understand material differences from the issue environment. | required |
| reproducible_steps | The repro report's commands, inputs, setup, and actions, read against the issue's reproduction steps. | Pass when the recorded setup and actions are complete enough for another person to understand and repeat the test that was actually performed. A cannot-reproduce attempt may pass when material differences or limitations that prevented an exact trigger are explicitly identified rather than hidden. | required |
| behavior_match | The recorded outputs, logs, screenshots, state changes, or other artifacts, read against the issue's described actual behavior and the report's stated outcome. | Pass when the artifacts either demonstrate the specific reported behavior, or clearly demonstrate what occurred during a valid cannot-reproduce attempt whose conclusion acknowledges that the issue behavior was not observed. A different or adjacent failure claimed as reproduction does not pass. | required |
| honest_outcome | The claim comment and repro report's conclusions, read against the recorded artifacts and the issue's expected and actual behavior. | Pass when the stated reproduced/cannot-reproduce outcome and any causal claims are supported by the evidence without overstating certainty; an evidenced cannot-reproduce result may pass. | required |
| repo_conventions | The claim comment and repro report, read against the issue context and repo-facts contribution, disclosure, and reporting policies. | Pass when the proposed comments comply with policies that apply to issue-thread contributions, including any required disclosure or conduct rules. Do not require a reproduction comment on an existing issue to repeat every field required for opening a new bug report unless the repository explicitly requires those fields in follow-up comments. | required |

## Verdict rule

Accept only when every required check passes. A failed or unclear required check results in reject. Preferred checks, if any are added later, may improve the report but never change the verdict.
