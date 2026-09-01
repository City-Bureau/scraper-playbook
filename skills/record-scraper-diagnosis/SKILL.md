---
name: record-scraper-diagnosis
description: Save an engineer-reviewed scraper diagnosis to Airtable or the configured work tracker without duplicating the same active failure. Use after diagnosis review when the destination schema and write authorization are known; do not investigate or repair the scraper.
---

# Record a Scraper Diagnosis

## Outcome

Create or update exactly one durable work record for an accepted scraper diagnosis, then verify the saved state.

This skill owns deduplication and intake. It does not decide whether the diagnosis is technically correct and does not change scraper code.

## Required Inputs

- engineer-reviewed diagnosis from `diagnose-scraper-alert` or an equivalent source;
- repository, spider, agency, failure class, source links, and observed time;
- current Airtable base/table/field mapping or equivalent work-tracker schema;
- statuses that count as active, resolved, or closed;
- reviewer, next owner, and requested initial status; and
- authorization to create or update the record.

Do not guess field IDs, status values, table names, or workspace-specific identifiers. Read the current schema through the supported connector or request the missing mapping.

## Workflow

### 1. Validate the handoff

Confirm that the diagnosis is marked reviewed and includes verified observations, preliminary or confirmed cause, confidence, estimate assumptions, and next action. Return incomplete drafts for review rather than filling gaps with guesses.

### 2. Search before creating

Search active records by repository and spider. Compare the failure class and current incident evidence.

Use `<repository>:<spider>:<failure-class>` as a candidate deduplication key:

- update an active record when it represents the same unresolved failure;
- create a new record when the prior failure is resolved or the failing boundary is materially different; and
- stop for reviewer judgment when the match is unclear.

Repeated alerts may update last-seen time, duration, impact, and evidence without creating a new request. Preserve the first-seen time and prior history.

### 3. Preview the write

Show whether the operation is `create` or `update`, the matching record if any, and the fields that will change. If the user did not explicitly request the write, ask for authorization at this point.

### 4. Write the durable record

Store only the fields supported by the current schema. Preserve:

- scraper, agency, repository, and failure class;
- first-seen and last-seen times;
- human-readable user impact;
- source alert and evidence links;
- reviewed diagnosis, status, confidence, and estimate assumptions;
- reviewer, owner, priority, and next action; and
- deduplication key or equivalent match fields.

Do not copy raw Slack threads, credentials, private headers, personal data, or unredacted logs into the record.

### 5. Verify the result

Re-read the saved record. Report its identifier or URL, whether it was created or updated, the deduplication decision, current owner and status, and any field that could not be stored.

## Stop Conditions

Stop when the diagnosis is not reviewed, schema or status values are unknown, write authorization is absent, the duplicate match is ambiguous, or the destination cannot be read back after writing.

Do not retry a create blindly after an uncertain response. Re-search using the deduplication fields before deciding whether another write is safe.
