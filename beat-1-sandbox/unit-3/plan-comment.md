My plan for #61 builds on my reproduction:
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-5904837825

In that run, the actual health_check handler passed the raw "SELECT 1"
string to SQLAlchemy 2.1.1, which rejected it; the handler logged the
textual-SQL error and reported postgres as unhealthy.

I plan to import text from sqlalchemy and wrap the probe in
text("SELECT 1") in api/routes/health.py.

I will add tests/unit/test_health.py with a regression test using
the real handler and an in-memory SQLite AsyncSession. Because CI
installs only the dev extras and aiosqlite is not declared, I will
also add "aiosqlite>=0.22.1" to the dev dependencies in pyproject.toml
so this test can run in CI. The test should
fail before the fix and pass afterwards, verifying that postgres is
healthy. A failure-control test will check that a failed database call
still reports postgres as unhealthy and raises HTTP 503.

I will repeat my Unit 2 reproduction and expect postgres to change
to healthy with no textual-SQL error. The overall response may remain
503 because the separate Redis bug #62 is outside this change.
I will run the repository checks and remove only test markers or
suppressions demonstrated to belong to #61.

This is limited to SQLAlchemy statement handling and the handler
with SQLite; I have not verified PostgreSQL or end-to-end HTTP.
I will build on fix/61-health-probe-text in my own fork.

ChatGPT helped draft this plan and will help draft the tests.
Claude Code will evaluate the plan. I will review the changes and
run the checks myself.
