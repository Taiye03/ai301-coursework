# Contribution: Add Markdown and HTML Summary Exporters

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.


**Contribution Number:** [1]
**Student:** Taiye Olomu
**GitHub Username:** Taiye03
**Issue:** https://github.com/Zwony/ecotrace/issues/183
**Pull Request:** Not opened yet

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

Unit 5: Building and refining an issue-scout for open-source contributions

I configured an issue-scout skill with a personalized fit profile, GitHub search queries, ranking rules, and a six-check rubric to discover and evaluate open-source issues. My initial scan returned 199 unique issues, but all five top-ranked candidates came from the same newly created repository because my ranking favored issues with few comments and recent updates. To improve the results, I prioritized issues at least seven days old, limited the top five to two issues per repository, and added maintainer responsiveness as a preferred rubric check to distinguish active repositories from those that engage with outside contributors. I documented these changes in scan-notes.md and graded additional issues individually, but I have not rerun the full scan to verify whether the revised ranking produces more diverse results.

**Unit 6: Using Voice Guard and repository memory to prepare a responsible open-source contribution**

I configured Voice Guard to check my GitHub communication against rules for issue claims, questions, and follow-up messages, and used it to review my claim before posting. When I tested a follow-up acknowledgment, the guard applied its initial-claim requirements to the reply and rejected the draft, revealing a limitation in how it distinguishes message types; I left that draft unposted rather than changing the rules without further testing. I also created a local CLAUDE.local.md for EcoTrace using its contribution guidelines and a scoped Claude Code investigation, which identified the relevant summary and exporter components without modifying the repository. I removed the template scaffolding and excluded the memory file through .git/info/exclude, keeping my personal notes out of the upstream pull request.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I found EcoTrace issue #183 while using my issue-scout tool to search for open-source contributions that matched my experience with Python and my interest in software engineering. My initial scan returned 199 unique issues, but all five top-ranked candidates came from the same newly created repository. After refining my search strategy and grading additional issues, I considered EcoTrace alongside several other projects. My scout gave EcoTrace #183 an accept verdict with moderate difficulty. I chose it because implementing Markdown and HTML summaries would allow me to work with an unfamiliar Python codebase, understand existing functionality, and practice writing tests while contributing a useful feature.

Before claiming the issue, I investigated whether EcoTrace was actively maintained or whether its recent activity was mainly related to Hacktoberfest. I found that the maintainer had been developing the project before October, although external contributions increased during Hacktoberfest. I also inspected core.py and noticed that get_summary() did not include total energy in kWh, even though the class tracks that value. This gave me a specific technical question to raise with the maintainer, who later confirmed that adding the energy field to the summary was the preferred approach. The issue-scout helped me narrow down my options, but its initial ranking showed me that recent updates and low comment counts were not enough to evaluate a repository. I would improve it further by incorporating longer-term maintenance activity and contributor response patterns.

Claim comment: https://github.com/Zwony/ecotrace/issues/183#issuecomment-6584948907

**Toolkit**

* Tool: issue-scout, using my customized fit profile, search strategy, and grading rubric.
* What it produced: An initial scan of 199 unique issues and a shortlist of candidates. EcoTrace #183 received an accept verdict with moderate difficulty after further evaluation.
* Difficulties: My initial ranking concentrated the top five results in one newly created repository. The scout also did not fully distinguish sustained maintenance activity from temporary increases in contributions.
* What changed: I prioritized issues at least seven days old, limited the top five results to two per repository, added maintainer responsiveness as a preferred check, and patched the rubric to assess scope feasibility. I also investigated EcoTrace’s maintenance history before claiming the issue.


---

## Understanding the Issue

**Problem Description**

EcoTrace tracks energy consumption and carbon emissions, but it does not currently provide the Markdown and HTML summary exporters requested in issue #183. This makes it harder for users to include readable summaries in documentation, reports, or web pages without formatting the data themselves.

**Expected Behavior**

Users should be able to generate a Markdown table or a self-contained HTML summary card using to_markdown() and to_html(). Both formats should include total energy consumption in kWh, tracking duration, and CO₂ emissions. The exporters should also handle missing or zero values without crashing.

**Current Behavior**

From my initial inspection of the repository, I found that get_summary() in ecotrace/core.py returns information such as tracking duration and total carbon emissions but does not include total_energy_kwh. However, the class already tracks energy consumption using self.total_energy_kwh. The requested Markdown and HTML exporters are not yet implemented. I have confirmed these observations through source inspection but have not yet reproduced the missing functionality in a local environment.

**Affected Components**

* ecotrace/core.py: Contains get_summary() and the tracked energy-consumption value. The maintainer confirmed that adding total_energy_kwh to the summary dictionary is an acceptable, backward-compatible approach.
* Export functionality: The new to_markdown() and to_html() methods need to be implemented in a location consistent with the project’s existing architecture. I will confirm the appropriate placement during local investigation.
* tests/test_exporters.py: The issue requests tests covering both exporters, including missing and zero values. The maintainer also requested tests for the updated summary.

**Toolkit**

* Tool: GitHub repository inspection and issue-scout. I used them to review the issue requirements, examine the existing implementation, and identify a design question for the maintainer.
* What it produced: I identified the missing energy field in get_summary() and confirmed that the class already tracks total energy consumption. I also received maintainer guidance approving the summary change.
* Difficulties: The issue describes the expected output but does not fully specify where the new exporters should be implemented. I have not yet validated the behavior locally.
* What changed: I asked the maintainer about adding total_energy_kwh to get_summary() and incorporated their response into my proposed approach. I will confirm the exporters’ placement when I inspect the local codebase.

---

## Reproduction Process

**Environment Setup**

I reproduced the missing functionality in EcoTrace issue #183 using my MacBook Air running macOS on Apple Silicon, Python 3.14.6, and EcoTrace 1.8.0 at baseline commit 05d9a12.

I cloned my fork of the repository, created a Python virtual environment, activated it, and installed EcoTrace in editable mode using python -m pip install -e ".[dev]".

During setup, pip warned that EcoTrace 1.8.0 does not provide a dev extra. I checked the project configuration and confirmed that its optional extras are gpu, ai, and web. To continue, I installed pytest 9.2.0 and flake8 7.5.0 separately.

Before investigating the requested functionality, I ran the existing test suite. The results were 251 passed and 2 skipped, with no failures. I also ran flake8 ecotrace/, which reported multiple pre-existing style violations. Because these issues were unrelated to the requested exporters, I documented them rather than modifying unrelated source files.

I completed the reproduction investigation without changing any EcoTrace source code.

**Steps to Reproduce**

1. Inspect the existing exporters. From the EcoTrace repository root at commit 05d9a12, I ran ls -la ecotrace/exporters/. The directory contained __init__.py, _retry_queue.py, cloud.py, otel.py, and webhook.py. No dedicated Markdown or HTML summary exporter module was present.
2. Search for the requested functions. I ran grep -RnE 'def (to_markdown|to_html)\(' ecotrace/. The command returned no matches, confirming that no functions with those names were defined in the searched source directory.
3. Verify the missing exporters at runtime. I imported ecotrace.exporters and checked whether it exposed to_markdown and to_html using Python’s hasattr(). Both checks returned False, confirming that neither function was available through the exporter package.
4. Inspect the session summary. I ran sed -n '539,615p' ecotrace/core.py to examine EcoTrace.get_summary(). The returned dictionary included session duration, carbon emissions, and other metadata, but did not include total_energy_kwh.
5. Confirm that energy is tracked internally. I ran grep -Rn 'self.total_energy_kwh' ecotrace/core.py. The output showed that the value is initialized at line 115 and accumulated at line 414. This confirmed that EcoTrace already maintains an internal energy-consumption value, even though get_summary() does not expose it.

Observed result: The requested Markdown and HTML summary exporters are not available at the baseline commit. Additionally, get_summary() omits the internally tracked total-energy metric needed for the requested summaries. This confirms that the requested feature has not yet been implemented; it does not indicate a regression in existing functionality.

**Reproduction Evidence**

* Commit showing reproduction: None. This is a feature request, and I confirmed the missing functionality through source inspection and runtime checks without modifying EcoTrace’s source code or creating a reproduction commit. The investigation was performed against baseline commit 05d9a12.
* Screenshots/logs: I collected terminal output showing that neither to_markdown nor to_html is exposed through ecotrace.exporters (False for both runtime checks). Searching the source directory found no function definitions with those names. The baseline test suite completed with 251 passed and 2 skipped. Flake8 reported existing style violations unrelated to this issue.
* My findings: The requested Markdown and HTML summary exporters have not yet been implemented. I also discovered that EcoTrace.get_summary() omits total_energy_kwh, even though the class initializes and updates that value internally. The maintainer confirmed that adding this field to the summary dictionary is acceptable, provided backward compatibility is maintained. This investigation established the missing functionality and identified the relevant code areas for implementation and testing.


**Toolkit**

* Tool: Claude Code’s repro-check skill, GitHub repository inspection, Python, pytest, and flake8.
* What it produced: I created a reproduction report documenting my environment, baseline tests, source-code inspection, runtime checks, and findings for EcoTrace issue #183. I then used repro-check to evaluate my claim draft and reproduction report. The grader returned an accept verdict, with all five checks passing: environment, reproducible steps, behavior match, honest outcome, and repository conventions.
* Difficulties: The project’s documented development installation command referenced a dev extra that was not defined in its configuration. I installed pytest and flake8 separately. The baseline linting command also reported existing style violations. Another challenge was distinguishing a missing feature from a regression, since the issue requests functionality that has not yet been implemented.
* What changed: I moved from understanding the issue requirements to verifying the repository’s actual behavior. I confirmed that the requested exporters were unavailable and identified the missing total_energy_kwh field in get_summary(). The reproduction investigation helped me understand which parts of the codebase need attention before implementation.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
