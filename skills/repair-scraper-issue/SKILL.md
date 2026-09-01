---
name: repair-scraper-issue
description: Repair an approved, tracked City Scraper issue from reproduction through tested pull request and production-validation handoff. Use when implementation is requested and the repository, source, work record, and reviewer are known; do not use for alert-only triage.
---

# Repair a Tracked Scraper Issue

## Outcome

Deliver the smallest safe, reviewed scraper change with evidence that it fixes the reproduced failure. Update the durable work record with the pull request and validation state when that write is authorized.

A merged pull request is not the final user outcome. The work closes only when production data is confirmed or a named follow-up owns that check.

## Required Inputs

- approved work record with current symptom and diagnosis status;
- repository, spider, authoritative public source, and expected behavior;
- repository guidance, tests, and deployment path;
- reviewer and production-validation owner; and
- authorization boundary for code, pull-request, and work-record writes.

If asked to choose the next item, rank active approved work using the team's current severity, user impact or coverage, age, and dependency rules. Show the proposed item and reasoning before beginning implementation.

## Workflow

### 1. Confirm scope and retrieve prior evidence

Read the work record, repository guidance, target spider and tests, recent relevant changes, and any reusable learnings for the source platform or failure class. Verify that the record still describes the current failure.

Preserve unrelated changes and work on a task branch or worktree according to repository rules.

### 2. Reproduce the failure

Compare the public source, live spider output, fixture and tests, and downstream product when available. Name the failing boundary in `file:line` or function terms and record the evidence.

If the preliminary diagnosis is wrong, update the draft diagnosis before patching. Do not force the code to fit the ticket.

### 3. Prove the regression check fails

Add or refresh the smallest safe fixture and assertion that represents the failure. Run it against the broken implementation and retain the failing result. Confirm that the test exercises the real entry path and fails for the intended reason.

### 4. Implement the smallest safe change

Follow current repository conventions. Explain each non-obvious parsing, filtering, pagination, status, or fallback rule with source evidence. State shared-code impact, malformed or empty-input behavior, unresolved limits, and rollback.

Never bypass source controls with private cookies, spoofed identities, or brittle circumvention.

### 5. Verify complete, correct, and current output

Run the repository's documented tests, lint, validation, and live crawl. Compare expected and actual meeting sets and fields, not only item counts. Check affected siblings when shared code changed.

Ask an independent reviewer—human, agent, or both—to challenge the source evidence, test strength, edge cases, and blast radius. Record each confirmed, rejected, or deferred finding.

### 6. Create the handoff

When external writes are authorized, create or update the pull request with:

- user problem and source;
- reproduced cause;
- files changed and why;
- failing-then-passing regression evidence;
- test, validation, and live-source results;
- review findings and dispositions;
- known limits and rollback; and
- deploy and production-validation owners.

Update the durable work record with the branch or pull request, current state, evidence, remaining owner, and any reusable learning candidate. Re-read the saved state to verify it. Do not mark the issue resolved before the agreed production check.

## Stop Conditions

Stop and hand off when the source of truth is ambiguous, credentials or questionable circumvention are required, the environment cannot reproduce or test the failure, shared infrastructure exceeds the approved scope, the proposed fix weakens validation, or a product/editorial decision is required.

Do not deploy, merge, or change production data unless the user has explicitly authorized that action and the repository's normal controls are available.
