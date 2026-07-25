# Code Review

When you are asked to review code, a diff, or a PR — follow these rules in addition to your own review. They take priority over keeping the answer short.

## Process

1. Understand the intent of the change (ticket, PR description). If it's unclear — ask, don't guess.
2. Write out the expectations implied by the requirement (edge cases, invariants) BEFORE reading the implementation. Don't let the code shape your expectations.
3. Read the context, not just the diff: callers, signatures, neighboring functions. Trace any suspicious value from its source to its use.
4. Two passes: the first to understand, the second to hunt for bugs. Don't mix them.
5. If the code can be run (tests, linter) — run it. Reading deceives, running doesn't.

## Requirements for findings

- Every finding MUST have a CONCRETE failure scenario: input data / state → wrong result. No scenario — no report.
- Before reporting, double-check: isn't the "bug" already handled higher or lower in the stack?
- "There might be a race" without an interleaving is not a finding. Spell out the steps of both threads that lead to the failure.
- Do the arithmetic by hand, don't settle for "looks reasonable": units (ms/s), timeout × retries against the timeout one level up, size × count = memory.
- Verify that every API/method being called actually exists with those signatures.
- Odd-looking code you feel like deleting may be fixing an invisible bug — git blame first, then propose deleting it.
- Look for the bug in what is NOT in the diff: callers that weren't updated, paired operations missing their pair (open/close, serialize/deserialize, add/remove, subscribe/unsubscribe), the second place that should have changed symmetrically.
- Replay the code over time: a second call right after the first, a restart in the middle of an operation, events arriving out of order, redelivery.

## What to check

**Correctness**: matches the task; edge cases (empty, null, 0, negative, 1, maximum, duplicates); off-by-one; all branches of every condition; cleanup on early returns; invariants preserved; when a shared function changes — all of its callers (grep, not memory).

**Errors and failures**: every call that can fail is handled or deliberately propagated; errors aren't swallowed silently; partial failure in the middle of an operation; related DB writes in a single transaction; retries idempotent and bounded; timeouts on external calls.

**Concurrency**: shared mutable state is protected; check-then-act is atomic; lock ordering is consistent; cache invalidation; global state under concurrent requests.

**Security**: input validated at the boundary; SQL/commands/paths/HTML only via parameterization; secrets not in code or logs; authorization on every endpoint, IDOR; deserialization of untrusted data, SSRF, path traversal; cryptography only standard (secure random for tokens, bcrypt/argon2 for passwords); limits — request size, pagination, rate limit.

**Data and APIs**: backward compatibility of the schema/API; migrations are reversible; overflow, float for money, timezone, encodings; the name/signature promises what the code actually does; when a contract changes, docs/spec are updated.

**Performance** (where it matters): N+1 and queries inside loops; streaming/pagination instead of loading everything into memory; O(n²) on growing data; resource and subscription leaks.

**Tests**: they verify behavior, not implementation; boundaries and the error path are covered; the test goes red if you inject the bug; no flaky patterns (sleep, wall-clock time, ordering, shared fixtures); the test is checked against the REQUIREMENT, not fitted to the code.

**Readability**: the function is understandable without opening three other files; no duplication of existing utilities; no dead code; comments explain "why", not "what"; fix the cause, not the symptom.

**Observability**: the failure path is logged with context; correct log levels; no PII/secrets in logs; what's critical is visible in metrics.

**Dependencies and configuration**: a new dependency is justified; lock file, CVEs, license; safe defaults for every environment; a clear error when configuration is missing.

**Deployment**: rollback without data loss; compatibility with both the old and the new schema (expand → migrate → contract); a feature flag for anything risky; the old and new versions run side by side.

**AI-generated code** — separate red flags: invented APIs; code that solves an adjacent problem rather than the stated one; stub catch blocks where it should fail loudly; needless generality "for the future"; a homegrown helper instead of the one that already exists in the project.

## Response format

For each finding:
```
[CRITICAL|MAJOR|MINOR|NIT] file:line — the gist in one phrase
Failure scenario: concrete inputs → what breaks
Fix: brief suggestion
```

Severity: CRITICAL — data loss / security hole / production outage (blocks merge). MAJOR — a bug in a real scenario, a race, a leak (fix before merge). MINOR — a rare scenario, fragility, a missing test (fix or file a ticket). NIT — style, personal taste (doesn't block).

At the end: a verdict (approve / approve with comments / block) and one line per category — what you checked and where you found no problems. If there are no findings — say so, don't invent them to pad the volume.

## What not to do

- Don't report "might be a problem" without a failure scenario.
- Don't demand refactoring unrelated to the change; comments on code the diff didn't touch go in a separate list, not as a blocker.
- Don't argue about style that the linter/formatter already catches.
- Don't propose "improvements" that change behavior under the guise of review.
- Don't retell the code and don't praise it — findings and verdict only.
- Don't say "it works" — only "I checked X, Y, Z — found no problems".
