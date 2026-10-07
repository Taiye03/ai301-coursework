# Plan for issue #61

## Issue and reproduction

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61

My reproduction:
https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61#issuecomment-5904837825

At commit 2f4e82f, I invoked the actual health_check handler with
SQLAlchemy 2.1.1 and an in-memory SQLite AsyncSession. It raised:
"Textual SQL expression 'SELECT 1' should be explicitly declared as text('SELECT 1')"
The handler reported postgres as unhealthy. Redis failed separately
because Settings has no redis_host attribute.

## Cause and proposed fix

The probe passes a plain SQL string to SQLAlchemy, which rejects it.
Import text from sqlalchemy in api/routes/health.py and change:
await db.execute("SELECT 1")
to:
await db.execute(text("SELECT 1"))

## Scope and steps

Use fix/61-health-probe-text in my own fork.

1. Add "aiosqlite>=0.22.1" to the dev dependencies in pyproject.toml.
   CI's test-unit job installs only .[dev], and aiosqlite is not
   currently declared, so the real SQLite AsyncSession regression
   test could not run in CI without it.
2. Add tests/unit/test_health.py. Call the actual health_check handler
   with a real in-memory SQLite AsyncSession and assert that the
   postgres dependency is healthy. Read the result from the returned
   body or HTTPException.detail, since Redis may still fail.
3. Run this regression test before changing the route; expect failure.
4. Add the text import and wrap the query.
5. Add a failure-control test using a mocked session whose execute
   raises a connection error. Assert postgres is unhealthy and HTTP
   503 is raised.
6. Run both tests and repeat my Unit 2 reproduction.
7. Run the lint, formatting, type, unit, and frontend checks required
   by CONTRIBUTING before pushing; record any blockers.

In scope: the text() fix in api/routes/health.py, the new test file,
and the aiosqlite dev dependency the test needs. Keep Redis issue #62,
vector-db behavior, exception policy, and unrelated cleanup out of
scope. Inspect health-related xfail markers
and suppressions; remove only those demonstrated to belong to #61.

## Expected results and limitations

Before: postgres is unhealthy and the textual-SQL error appears.
After: postgres is healthy and that error disappears.
The overall response may remain 503 because Redis is still unhealthy.
A failed database call must still report postgres as unhealthy.

This tests SQLAlchemy and the handler with SQLite. I have not verified
PostgreSQL or an end-to-end HTTP request.

Other classmates' plans do not block my own plan under the classroom
house rules. This plan builds on my own posted reproduction.

ChatGPT helped draft this plan and will help draft tests.
Claude Code will evaluate the plan. I will review the changes and
run the checks myself.

## Deviations

The posted plan held. I added the aiosqlite dev dependency, wrapped the
probe with text(), added the real-session regression and failure-control
tests, and repeated my Unit 2 reproduction.

The regression failed before the fix and passed afterwards. I combined
nested test context managers to satisfy Ruff without changing behavior.

No health-test xfail marker needed removal. Existing mypy suppressions
still cover dictionary typing and Redis findings, so I kept them.
Redis #62, vector-db behavior, and exception policy remain unchanged.

Lint, typecheck, unit tests, frontend tests, and formatting of the changed
Python files passed. PostgreSQL, end-to-end HTTP, integration tests,
and remote CI remain unverified.
