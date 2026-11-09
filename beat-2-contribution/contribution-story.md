# Contribution: Add Markdown and HTML Summary Exporters

**Contribution Number:** [1]
**Student:** Taiye Olomu
**GitHub Username:** Taiye03
**Issue:** https://github.com/Zwony/ecotrace/issues/183
**Pull Request:** https://github.com/Zwony/ecotrace/pull/252

## Toolkit

**Unit 5: Building and refining an issue-scout for open-source contributions**

I configured an issue-scout skill with a personalized fit profile, GitHub search queries, ranking rules, and a six-check rubric to discover and evaluate open-source issues. My initial scan returned 199 unique issues, but all five top-ranked candidates came from the same newly created repository because my ranking favored issues with few comments and recent updates. To improve the results, I prioritized issues at least seven days old, limited the top five to two issues per repository, and added maintainer responsiveness as a preferred rubric check to distinguish active repositories from those that engage with outside contributors. I documented these changes in scan-notes.md and graded additional issues individually, but I have not rerun the full scan to verify whether the revised ranking produces more diverse results.

**Unit 6: Using Voice Guard and repository memory to prepare a responsible open-source contribution**

I configured Voice Guard to check my GitHub communication against rules for issue claims, questions, and follow-up messages, and used it to review my claim before posting. When I tested a follow-up acknowledgment, the guard applied its initial-claim requirements to the reply and rejected the draft, revealing a limitation in how it distinguishes message types; I left that draft unposted rather than changing the rules without further testing. I also created a local CLAUDE.local.md for EcoTrace using its contribution guidelines and a scoped Claude Code investigation, which identified the relevant summary and exporter components without modifying the repository. I removed the template scaffolding and excluded the memory file through .git/info/exclude, keeping my personal notes out of the upstream pull request.

**Unit 7: Using Ship Gate and a custom test manifest to verify my contribution before submission**

I configured Ship Gate with a manifest that runs EcoTrace’s Python test suite and uses my PR precheck rubric to evaluate plan fidelity, test evidence, diff quality, and communication standards. My initial gate run passed the tests but rejected the contribution because it incorrectly identified existing Prometheus exporter code as unrelated changes. I investigated the Git history and discovered that my local main branch was outdated; after fetching upstream changes, confirming there were no unique local commits, and aligning main with upstream/main, I reran the gate. Ship Gate then returned PASS, confirming that the six-file contribution satisfied all four rubric checks and that the Python test suite passed.

**Unit 8: Configuring PR Monitor and reviewing an AI-generated follow-up**

I configured PR Monitor with a personal playbook covering response rules, staleness thresholds, nudge etiquette, and walk-away criteria. I examined five merged EcoTrace pull requests to understand maintainer response times and selected five quiet days as my follow-up threshold. I ran PR Monitor against my merged PR #252, which detected 11 passing checks and generated a close-of-loop message thanking the maintainer, mentioning issue #183, and suggesting a possible follow-up for existing lint violations. After reviewing the draft, I decided not to post it because I had already thanked the maintainer and the additional suggestions were unnecessary.

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

From my initial inspection of the repository, I found that get_summary() in ecotrace/core.py returns information such as tracking duration and total carbon emissions but does not include total_energy_kwh. However, the class already tracks energy consumption using self.total_energy_kwh. The requested Markdown and HTML exporters are not yet implemented. I confirmed these observations through local source inspection and runtime checks, which showed that neither exporter was available and that get_summary() omitted the existing energy metric.

**Affected Components**

* ecotrace/core.py: Contains get_summary() and the tracked energy-consumption value. The maintainer confirmed that adding total_energy_kwh to the summary dictionary is an acceptable, backward-compatible approach.
* Export functionality: The new to_markdown() and to_html() methods need to be implemented in a location consistent with the project’s existing architecture. I will confirm the appropriate placement during local investigation.
* tests/test_exporters.py: The issue requests tests covering both exporters, including missing and zero values. The maintainer also requested tests for the updated summary.

**Toolkit**

* Tool: GitHub repository inspection and issue-scout. I used them to review the issue requirements, examine the existing implementation, and identify a design question for the maintainer.
* What it produced: I identified the missing energy field in get_summary() and confirmed that the class already tracks total energy consumption. I also received maintainer guidance approving the summary change.
* Difficulties: The issue describes the expected output but does not fully specify where the new exporters should be implemented. I subsequently validated the missing functionality through local source inspection and runtime checks.
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

EcoTrace issue #183 is a feature request rather than a bug or regression. The application already tracks cumulative energy consumption through self.total_energy_kwh in ecotrace/core.py, but get_summary() does not include this value in its returned dictionary. As a result, downstream consumers cannot retrieve total energy consumption directly from the session summary.

Additionally, the ecotrace/exporters/ package currently provides cloud, OpenTelemetry, and webhook exporters but does not include the requested Markdown and HTML summary generators. The maintainer confirmed that adding total_energy_kwh directly to get_summary() is the preferred backward-compatible approach.

**Proposed Solution**

I will update get_summary() to include the existing total_energy_kwh value while preserving all current summary fields.

I will implement lightweight to_markdown() and to_html() utilities that generate readable reports from session summary data. Both formats will display total energy consumption in kWh, tracking duration in seconds, and carbon emissions in gCO₂eq.

The formatting utilities will handle missing and zero values without crashing. The HTML output will also escape any user-provided text included in the report.

I will follow the repository’s existing conventions and confirm the appropriate function signatures and public import paths before implementation.

I will not modify the existing energy calculations, carbon accumulation logic, unrelated exporters, or pre-existing repository-wide lint violations.

**Implementation Plan**

1. Update ecotrace/core.py to add total_energy_kwh to the dictionary returned by get_summary() and document the new field.
2. Implement to_markdown() and to_html() within ecotrace/exporters/, using the session summary data to generate Markdown and standalone HTML reports.
3. Update the exporter package’s public interface as needed to expose the new utilities.
4. Add unit tests in tests/test_exporters.py to verify Markdown and HTML formatting, required metrics, and handling of missing and zero values.
5. Add tests confirming that get_summary() includes total_energy_kwh without removing existing fields.
6. Run the existing pytest suite, verify the new functionality, and check modified code for lint issues. Document any pre-existing failures separately.

Any changes to this plan during implementation will be recorded in the Implementation Notes section.

**Toolkit**

* Tool: Claude Code, GitHub CLI, terminal commands, and manual source-code inspection.
* What it produced: An investigation of the existing energy tracking, summary dictionary, exporter architecture, and test conventions, resulting in a proposed implementation plan.
* Difficulties: The issue specifies the required output formats but does not define exact function signatures or import paths.
* What changed: I incorporated the maintainer’s guidance to expose the existing energy value through get_summary() rather than introducing a new calculation. The exporter API will be confirmed before implementation.

---

## Testing Strategy

I used baseline reproduction checks, targeted unit tests, the full pytest suite, lint inspection, and Ship Gate to verify my implementation.

**Baseline Verification**

Before implementing the feature, I inspected the exporter package and searched for to_markdown() and to_html(). Neither function was available. I also confirmed that get_summary() did not expose total_energy_kwh, although EcoTrace already tracked that value internally.

The baseline test suite completed with 251 passed and 2 skipped, establishing that the existing functionality worked before my changes.

**Feature Verification**

After implementation, I verified that:

1. to_markdown() generates a readable Markdown summary containing energy consumption, tracking duration, and carbon emissions.
2. to_html() generates a standalone HTML summary containing the same metrics.
3. Both exporters handle missing and zero values without crashing.
4. HTML output escapes user-provided text to prevent unintended HTML interpretation.
5. get_summary() exposes total_energy_kwh while preserving existing fields and their order.
6. The new utilities are accessible through the exporter package’s public interface.

I added automated tests in tests/test_exporters.py and tests/test_core.py to verify these behaviors.

**Regression Testing**

I ran the full pytest suite at multiple stages of implementation.

* Baseline: 251 passed, 2 skipped.
* After initial implementation: 290 passed.
* After integrating upstream changes: 1 failed, 304 passed. I investigated and corrected the failure.
* Final verified run: 305 passed, 2 skipped.

I also ran lint checks and compared the reported violations against the upstream baseline. The repository contained pre-existing flake8 violations, which I documented rather than modifying unrelated code.

**Final Ship Gate Verification — November 7, 2026**

I configured Ship Gate to run the repository’s Python test suite and evaluate my contribution against four PR precheck criteria: plan fidelity, test evidence, diff quality, and standards and communication.

The first run passed pytest but failed the PR precheck because my local main branch was outdated. The comparison incorrectly included Prometheus exporter changes that were already present upstream.

After updating the comparison baseline to upstream/main, I verified that my contribution affected only six intended files and reran Ship Gate.

The final result was PASS, with all four precheck criteria accepted. Ship Gate also completed its Python test suite successfully in approximately 67 seconds.

**Toolkit**

* Tool: pytest, flake8, Git, Claude Code’s PR precheck, and Ship Gate with a custom ship-manifest.md.
* What it produced: Automated regression results, test evidence, a six-file diff verification, and a final Ship Gate PASS confirming that the contribution satisfied the configured checks.
* Difficulties: The repository contained pre-existing lint violations, an upstream integration initially caused a test failure, and an outdated local main branch caused Ship Gate to incorrectly identify unrelated Prometheus changes.
* What changed: I fixed the integration failure, documented existing lint limitations, investigated the Git comparison, aligned my local main with upstream/main, and reran Ship Gate successfully.

---

## Implementation Notes

**November 2026 — Implementation and Initial Testing**

I implemented the Markdown and HTML summary exporters for EcoTrace issue #183 using Claude Code to assist with repository investigation and development.

I updated get_summary() in ecotrace/core.py to include the existing total_energy_kwh value without changing the energy calculations or removing existing summary fields.

I added ecotrace/exporters/summary.py with to_markdown() and to_html() utilities. The Markdown exporter produces a readable table, while the HTML exporter produces a standalone summary card. Both support missing and zero values, and the HTML implementation escapes user-provided text.

I updated the exporter package’s public interface, added tests in tests/test_exporters.py and tests/test_core.py, and documented the new functionality in the README.

The initial implementation passed 290 tests.

**November 2026 — Upstream Integration and Regression Fix**

While preparing the contribution, I integrated newer changes from the upstream repository.

The integration initially produced one failing test, with 304 tests passing. I investigated the failure and corrected it rather than assuming that the new exporters were responsible.

After the correction, the full test suite completed with 305 passed and 2 skipped.

I also compared lint findings against the upstream baseline and documented existing repository-wide violations rather than expanding the scope of my contribution.

**November 7, 2026 — Maintainer Review and Follow-up**

After opening PR #252, I received encouraging feedback from the EcoTrace maintainer, who described the contribution as well crafted and thoroughly tested.

The maintainer identified a duplicate WebhookExporter entry in ecotrace/exporters/__init__.py and requested that I remove it before merging.

I removed the duplicate entry, verified the change, reran the test suite, and pushed commit f6ed9ff to my feature branch.

I also replied to the maintainer on GitHub to acknowledge the feedback and explain what I had changed.

The PR’s automated checks subsequently passed.

**November 7, 2026 — Ship Gate Verification**

I configured Ship Gate with a manifest that runs the repository’s Python test suite and uses my PR precheck rubric to evaluate the contribution.

The first run passed the Python tests but rejected the PR because it incorrectly included unrelated Prometheus exporter changes in the comparison.

I investigated the Git history and discovered that my local main branch was behind upstream/main.

After fetching upstream changes, confirming that my local main contained no unique commits, and updating it to match upstream/main, I verified that the PR diff contained only six intended files.

I reran Ship Gate, which returned PASS across all four precheck categories.

**November 7, 2026 — Pull Request Approved and Merged**

After addressing the maintainer’s feedback and pushing the correction in commit f6ed9ff, the maintainer reviewed the updated pull request and confirmed that the duplicate exporter entry had been removed and that all CI and security checks were passing.

The maintainer approved PR #252 and merged it into EcoTrace’s main branch on November 7, 2026.

This marked the completion of my first open-source contribution, from investigating issue #183 and implementing the requested functionality to writing tests, addressing review feedback, and having my changes accepted into the upstream repository.

**November 9, 2026 — PR Monitor and Post-Merge Review**

I configured PR Monitor with a personal playbook based on EcoTrace’s contribution guidelines and the response times of five previously merged pull requests. I ran the monitor against my merged PR #252, which detected 11 passing checks and generated a suggested close-of-loop message.

After reviewing the draft, I decided not to post it because I had already thanked the maintainer and the contribution was complete. This demonstrated the importance of reviewing AI-generated recommendations before taking action.

**Toolkit**

* Tool: Claude Code, Git, GitHub CLI, pytest, flake8, Ship Gate, and PR Monitor.
* What it produced: Markdown and HTML exporters, updated summary data, automated tests, README documentation, a merged pull request, successful Ship Gate verification, and a PR Monitor follow-up draft.
* Difficulties: Upstream integration introduced a test failure, the maintainer identified a duplicate exporter entry, an outdated Git branch caused Ship Gate to flag unrelated changes, and PR Monitor suggested a follow-up message that was unnecessary after the merge.
* What changed: I fixed the integration failure, removed the duplicate exporter entry, synchronized my Git comparison baseline, and reran Ship Gate successfully. I also reviewed the PR Monitor draft and chose not to post it because I had already thanked the maintainer.

---

## Pull Request

**PR Link:** https://github.com/Zwony/ecotrace/pull/252

**PR Description:** PR #252 resolves issue #183 (https://github.com/Zwony/ecotrace/issues/183) by adding Markdown and HTML summary exporters to EcoTrace. It implements to_markdown() and to_html() in ecotrace/exporters/summary.py and adds total_energy_kwh to the dictionary returned by get_summary(), the backward-compatible approach the maintainer confirmed before implementation. The PR also includes automated tests for both exporters and the updated summary, plus README documentation of the new functionality. The final regression run completed with 305 passed and 2 skipped.

**Maintainer Feedback:**

- November 7, 2026: The maintainer described the contribution as well crafted and thoroughly tested, and requested that I remove a duplicate WebhookExporter entry in ecotrace/exporters/__init__.py before merging.
- November 7, 2026: I removed the duplicate entry in commit f6ed9ff, pushed it to my feature branch, and replied to the maintainer on GitHub to explain the change. All CI and security checks passed.
- November 7, 2026: The maintainer approved PR #252 and merged it into main.

**Status:** Merged

**Toolkit**

- Tool: GitHub (the PR #252 review thread and its CI and security checks) and Git, which I used to commit and push the requested fix; Ship Gate with my PR precheck rubric for pre-merge verification.
- What it produced: A reviewed pull request, the follow-up commit f6ed9ff removing the duplicate WebhookExporter entry, a reply to the maintainer, passing CI and security checks, and finally an approved and merged PR.
- Difficulties: The maintainer found a duplicate WebhookExporter entry during review that I had missed before opening the PR.
- What changed: I removed the duplicate entry, replied to the maintainer, and confirmed all checks passed before the merge. Next time I would review the diff of package export files such as __init__.py more carefully for duplicated entries before requesting review.

---

## Learnings and Reflections


**Technical Skills Gained**

This contribution strengthened my ability to navigate an unfamiliar Python codebase, understand its architecture, and implement new functionality while maintaining backward compatibility. I gained practical experience building Markdown and HTML exporters, handling missing and zero values, escaping HTML content, and extending an existing public API.

I also improved my testing and debugging skills by writing targeted unit tests, running regression tests, and investigating failures after integrating upstream changes. Working with Git helped me better understand branch comparisons, upstream synchronization, and how an outdated local branch can affect automated code reviews.

Beyond implementation, I gained experience with the complete open-source workflow, from identifying an issue and communicating with a maintainer to submitting a pull request, responding to feedback, and getting my changes merged.

**Challenges Overcome**

One of my first challenges was identifying a suitable issue. My initial issue-scout scan returned 199 unique issues, but the ranking concentrated the top results in one newly created repository. I refined the ranking criteria and investigated EcoTrace’s maintenance history before selecting issue #183.

During development, I encountered a test failure after integrating upstream changes. I investigated and corrected the failure, eventually achieving 305 passing tests and 2 skipped tests.

Another challenge occurred when Ship Gate incorrectly identified unrelated Prometheus exporter changes because my local main branch was outdated. After investigating the Git history and updating the comparison baseline, I reran Ship Gate successfully.

The maintainer also identified a duplicate WebhookExporter entry that I had overlooked. I removed the duplicate, verified the correction, and pushed an updated commit. The PR was subsequently approved and merged.

**What I’d Do Differently Next Time**

For my next contribution, I would inspect the repository’s development setup, contribution guidelines, and recent upstream changes earlier in the process. I would also ensure my local comparison branch is synchronized with upstream before running automated reviews.

I would review changes to public export files more carefully before opening a pull request. Although my tests passed, the duplicate WebhookExporter entry demonstrated that automated tests cannot replace a careful manual review.

I would continue using AI-assisted development tools while independently verifying their recommendations. My experience with issue-scout, Voice Guard, Ship Gate, and PR Monitor showed that these tools can be useful but may make incorrect assumptions or suggest actions that are unnecessary.

Finally, I would continue documenting decisions, failures, and feedback throughout the contribution process. Keeping detailed records helped me understand my progress and explain how I approached problems rather than focusing only on the final implementation.

---

## Resources Used

* EcoTrace Issue #183: https://github.com/Zwony/ecotrace/issues/183 — Provided the feature requirements and maintainer guidance on adding total_energy_kwh to get_summary().
* EcoTrace Pull Request #252: https://github.com/Zwony/ecotrace/pull/252 — Documented my implementation, maintainer feedback, requested correction, automated checks, approval, and merge.
* EcoTrace CONTRIBUTING.md: Helped me understand the repository’s contribution guidelines and communication expectations.
* EcoTrace source code and test suite: I examined ecotrace/core.py, ecotrace/exporters/, and the existing tests to understand the architecture and implement the requested functionality.
* Python, pytest, and flake8: Used for local development, regression testing, and lint inspection.
* Git and GitHub CLI: Used to manage branches, inspect repository history, compare changes, and review pull request activity.
* Claude Code and CodePath AI301 toolkit: Used issue-scout for issue discovery, repro-check for reproduction verification, Voice Guard for communication review, Ship Gate for pre-merge verification, and PR Monitor for post-merge review.
