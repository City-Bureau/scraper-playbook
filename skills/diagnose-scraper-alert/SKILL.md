---
name: diagnose-scraper-alert
description: Turn a broken or degraded scraper alert into an evidence-backed preliminary diagnosis and effort range for engineer review. Use for triage before implementation; do not use this skill to write work records or change scraper code.
---

# Diagnose a Scraper Alert

## Outcome

Produce a diagnosis draft that an engineer can review. Leave durable-system writes to the `record-scraper-diagnosis` skill after the draft is accepted.

An alert reports a symptom. Do not present its wording as a confirmed cause.

## Required Inputs

- alert or digest item, including observed time and human-readable impact;
- scraper name, agency, repository, and public source when known;
- access to relevant run status or logs, current code, and user-facing output;
- person responsible for reviewing the diagnosis.

If the scraper identity or public source cannot be established, stop and request the missing input.

## Workflow

### 1. Preserve the reported facts

Record the alert text, observed time, severity, duration, affected meetings or assignments, and links. Separate reported facts from interpretations.

### 2. Note possible existing work

If a work tracker is available read-only, search open and in-progress work for the same repository and spider so the reviewer can see possible matches. Do not decide or write the durable record in this skill.

Compare the failure class as well as the scraper name. Useful classes include:

- no recent activity or unexpected silence;
- scheduled run failure;
- empty result;
- schema or ingestion rejection;
- incorrect or unusable meeting data; and
- duplicate, stale, or misassigned meetings.

Treat `<repository>:<spider>:<failure-class>` as a candidate deduplication key and include possible matching records in the draft. The intake skill will decide whether to create or update after review.

### 3. Gather the minimum evidence

Check, when available:

- the authoritative public source and expected meetings;
- the latest spider run status, output, and relevant error;
- the current spider and recent changes;
- committed fixtures and tests; and
- whether valid output reached the correct agency in the product.

Do not require production credentials for ordinary diagnosis. Never copy tokens, cookies, private headers, or raw private logs into the work record.

### 4. Draft the diagnosis

State:

- user impact and current severity;
- verified observations;
- likely failing boundary and supporting evidence;
- alternative explanations not yet ruled out;
- confidence: low, medium, or high;
- next check needed to confirm the cause;
- effort range with assumptions, not false precision; and
- recommended owner or skill for the next step.

Use `file:line` or function references only when inspected. If the failure has not been reproduced, label the cause as preliminary.

### 5. Hand the draft to an engineer

Present the diagnosis draft and any possible matching records. Do not create or materially update Airtable, an issue tracker, or another durable system. After the engineer accepts or revises the draft, use `record-scraper-diagnosis` for the deduplicated write.

## Output

```markdown
# Preliminary scraper diagnosis

- Scraper / agency:
- Alert and observed time:
- User impact:
- Existing work record:
- Failure class / deduplication key:
- Verified observations:
- Likely failing boundary:
- Alternatives still open:
- Confidence:
- Estimate range and assumptions:
- Next confirming check:
- Reviewer / next owner:
```

## Stop Conditions

Stop and hand off when source authority is unclear, access requires sensitive credentials, the scraper identity is ambiguous, evidence conflicts across systems, or the request has expanded from diagnosis into a write or implementation without authorization.

Scheduling, Slack access, GitHub access, and work-tracker access are platform capabilities—not guarantees made by this skill. If a connector or routine is unavailable, return the draft and a clear handoff instead of inventing evidence.
