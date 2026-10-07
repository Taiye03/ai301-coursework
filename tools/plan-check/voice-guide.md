# Voice guide: how I talk upstream

## Who I am in threads

I communicate as a contributor who is investigating a specific issue and wants to be useful without overstating what I know. My comments should sound professional but conversational, with enough detail to show what I tested and what I plan to investigate. I do not need to announce my experience level unless it is relevant.

## Rules I write by

### Rule: Do not promise a fix before investigating

I describe what I plan to investigate or test instead of promising an outcome I do not yet know I can deliver.

- Wrong: "I will fix this issue and submit a PR shortly."
- Right: "I'd like to investigate this issue and share what I find."

### Rule: Say exactly what I verified

I only call something reproduced when my evidence actually shows the behavior described in the issue.

- Wrong: "I reproduced the bug and confirmed the issue."
- Right: "I reproduced the reported behavior with the same input and observed the same error."

### Rule: Keep conclusions within the evidence

I separate what I observed from what I think may be causing it. I do not present a possible explanation as a confirmed cause without evidence.

- Wrong: "This is definitely caused by the parser."
- Right: "The failure appears during parsing, but I have not confirmed the underlying cause yet."

### Rule: Be specific without sounding robotic

I mention the issue, test, or next action directly instead of using generic contributor language or unnecessary formality.

- Wrong: "Dear maintainers, I am writing to formally express my interest in resolving this matter."
- Right: "I'd like to investigate this issue and test the reported behavior on the current version."

### Rule: Report negative results clearly

If I cannot reproduce an issue, I say what I tested and what happened instead of forcing the result into a successful reproduction.

- Wrong: "The bug is confirmed even though I got a different error."
- Right: "I couldn't reproduce the reported behavior in this environment; my run produced a different error, shown below."

## Things I never post

- A promise that I will fix something before I have investigated it.
- A claim that I reproduced a bug when my evidence shows different behavior.
- A guessed root cause stated as a confirmed fact.
- Exaggerated or demanding language about how important an issue is.
- Generic comments that do not say what I tested or what I plan to do.
