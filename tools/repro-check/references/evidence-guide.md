# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In an eval package, look at the issue's stated environment, the repo-facts block for required environment information, and the environment details recorded in the candidate repro report. In live mode, compare the GitHub issue and repository reporting requirements with the environment recorded in the draft repro comment.

What good looks like: The report identifies the versions, platform, installation or build details, and other environment facts that materially affect the issue. Differences from the reporter's environment are acceptable when they are made clear and still allow the result to be interpreted.

## Steps

Where it lives: In an eval package, compare the issue's reproduction instructions with the commands, inputs, setup, and actions recorded in the repro report. In live mode, compare the GitHub issue's trigger conditions with the steps in the student's draft.

What good looks like: Another person can determine the starting state, perform the relevant actions, and reach the tested condition without having to guess a material step. Inputs and commands preserve the conditions that matter to the reported bug.

## Behavior shown

Where it lives: Look at the issue's description of actual behavior and compare it directly with artifacts in the repro report, such as terminal output, logs, screenshots, resulting files, or observable application state.

What good looks like: The artifacts demonstrate the specific behavior at issue, not merely another error or nearby failure. If the reported behavior does not occur, the evidence should still clearly show what happened under a valid reproduction attempt.

## Honesty

Where it lives: Compare statements in the claim comment and repro report, especially reproduced or cannot-reproduce conclusions and causal explanations, with the commands, outputs, logs, and other artifacts that support them.

What good looks like: Conclusions say no more than the evidence establishes. A supported cannot-reproduce result is valid; unsupported certainty, guessed causes presented as facts, or claiming reproduction when the evidence shows different behavior is not.

## Comms

Where it lives: In an eval package, compare the claim comment and repro report with the issue context, repo-facts reporting requirements, contribution policy, and any stated AI-use disclosure requirement. In live mode, check the issue thread and repository contribution/reporting documentation against the student's draft comments.

What good looks like: The comments are specific to the issue, accurately describe what the contributor has done or plans to do, provide information required by the repository, and follow stated contribution and disclosure rules. They avoid unsupported claims, misleading promises, and generic boilerplate that could apply to any issue.
