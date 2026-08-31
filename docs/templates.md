# CtD Scraper Agent — Templates

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Templates](templates.md)

Copy these into an issue, pull request, case record, or future shared repository. Delete fields that do not help; add fields only when the team will use them.

## First 30 Minutes

```markdown
# Task start

- Task owner:
- Reviewer:
- Build or repair:
- Agency/body:
- Authoritative public source:
- User-visible success:
- Production-validation owner:

## Environment

- Repository and task branch:
- Repository guidance read:
- Similar current spiders/tests read:
- Tests and live crawl runnable:
- Browser or HTTP source access available:
- Missing capability and handoff owner:

## Ground truth

- Expected meetings/date window:
- Important edge cases:
- Fields verified from source:
- Source/body exclusions:

## Boundaries

- Files in scope:
- Systems that are read-only:
- Required checks:
- Stop/escalate conditions:

## Plan

1.
2.
3.
```

## Scraper Contract

```markdown
# Scraper contract: <agency/body>

Status: Draft | Reviewed | Active | Superseded
Owner:
Reviewer:
Last checked:

## User outcome

Who needs these meetings, and what action depends on them?

## Scope

- Included body/bodies:
- Excluded body/bodies:
- Date window:
- Timezone:

## Source authority

| Field | Authoritative public source | Notes |
| --- | --- | --- |
| Meeting set | | |
| Title/body | | |
| Start/end | | |
| Cancellation/status | | |
| Location/remote access | | |
| Agenda/minutes/video | | |

## Expected behavior

- Pagination/list-detail behavior:
- Legitimate empty period:
- Unexpected empty or malformed source behavior:
- Duplicate prevention:
- Agency identity/matching expectation:

## Complete, correct, current checks

- Complete:
- Correct:
- Current:
- Downstream/production confirmation:

## Known limits

-
```

## Repair Record

```markdown
# Repair: <spider and symptom>

- Owner:
- Reviewer:
- Detected at:
- Signal/report:
- User impact:
- Public source:

## Reproduction

| Surface | Observed result | Evidence |
| --- | --- | --- |
| Live source | | |
| Spider output | | |
| Fixture/tests | | |
| Ingestion/product | | |

## Diagnosis

- Failing boundary and file/function:
- Old assumption:
- Current source behavior:
- Blast radius and siblings:
- Non-code causes considered:

## Safe change

- Files changed:
- Smallest-fix rationale:
- Failure behavior:
- Rollback:

## Regression evidence

- New/updated test:
- Failing result before fix:
- Passing result after fix:
- CI-equivalent checks:

## Review

| Finding | Evidence checked | Disposition | Follow-up |
| --- | --- | --- | --- |
| | | | |

## End-to-end validation

- Expected versus actual meetings:
- Correct agency confirmed:
- Production/public result:
- Confirmed at/by:

## Remaining limits and owner

-

## Learning candidates

-
```

## Reusable Learning Record

```markdown
# Learning: <short reusable statement>

- Status: Candidate | Available | Hidden | Disabled | Retired
- Scope: Source | Repository | Platform | Framework | Operating practice
- Owner:
- Reviewer:
- Created/updated:

## Context

- Source/platform:
- Repository/framework:
- Task or failure shape:

## Evidence

- Public source:
- Ticket/PR:
- Test or validation result:
- Related case:

## Learning

What should future work consider?

## How to use it

What context should retrieve it, and what must be re-verified?

## Limits and counterexamples

-

## Control history

| Date | Actor | Change | Reason |
| --- | --- | --- | --- |
| | | | |
```

## Review and Handoff

```markdown
# Review and handoff: <task>

## Why

- User problem:
- Scope:
- Authoritative source:

## What changed

- Files/components:
- Design choice:
- Shared-code impact:

## Evidence

- Fixture date/sanitization:
- Tests and validators:
- Live crawl:
- Expected-versus-actual comparison:

## Adversarial review

| Finding | Confirmed? | Evidence | Resolution |
| --- | --- | --- | --- |
| | | | |

## Limits

- Unverified assumptions:
- Known exclusions:
- Monitoring gap:

## Ownership

- Merge owner:
- Deploy owner:
- Production-validation owner:
- Follow-up date:

## Reusable learnings

- Candidate records:
```

## Shared `SKILL.md` Pattern

Use this as a structural pattern, not a product-specific promise.

Before turning it into a discoverable skill, verify the target agent platform's required metadata, directory, naming, and discovery rules in current authoritative documentation.

```markdown
# <Skill name>

## Purpose

What repeatable outcome does this guidance support?

## Use when

-

## Do not use when

-

## Required inputs

- Repository/source/task evidence:
- Human owner and reviewer:

## Safe boundaries

- Read-only systems:
- Files/actions in scope:
- Secrets and private data rules:
- Stop/escalate conditions:

## Workflow

1. Inspect repository guidance and similar current work.
2. Establish or reproduce live ground truth.
3. State the plan, assumptions, and blast radius.
4. Make the smallest reviewable change.
5. Run repository checks and live-source comparison.
6. Prepare evidence-rich review and handoff.
7. Capture reviewable learning candidates.

## Required outputs

-

## Human gates

- Scope approval:
- Merge:
- Deploy:
- Production validation:

## References and evidence

-

## Change control

- Owner:
- Review path:
- Disable/revert method:
- Last verified:
```

## Optional Case or Session Summary

Do not paste a raw session transcript into Git.

```markdown
# Case summary: <task>

- Date:
- Participants/roles:
- Public source:
- Ticket/PR:

## Problem and boundary

-

## Important evidence and decisions

-

## What changed and how it was verified

-

## Review findings

-

## Outcome and remaining limits

-

## Learning candidates

-

## Privacy check

- [ ] No credentials, tokens, cookies, or private headers
- [ ] No unnecessary personal data
- [ ] No raw private transcript or confidential content
- [ ] Access-controlled sources are linked, not copied
```
