# Workflow Skills: From Alert to Repair

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Skills](workflow-skills.md) · [Templates](templates.md)

## The Workflow

A scraper alert can explain a problem clearly and still be a poor place to track work. Slack threads move out of view, repeated alerts can create duplicate requests, and a preliminary diagnosis can be mistaken for a confirmed cause.

Keep four parts separate:

| Part | Purpose |
| --- | --- |
| Digest or alert | Signals a possible problem and explains its user impact |
| Diagnosis skill | Checks the evidence and drafts a diagnosis and effort range |
| Intake skill and durable work record | Deduplicates accepted diagnoses and tracks ownership, status, and evidence |
| Repair skill | Reproduces, fixes, reviews, and validates an approved item |

A routine or event trigger can decide **when** to run a skill. A connector can provide access to Slack, GitHub, or Airtable. Neither replaces the skill, which defines **how** to do the work. Verify scheduling and connector capabilities in the chosen agent platform before relying on them.

## What Makes a Useful `SKILL.md`

A shared skill should help an agent make better decisions, not repeat a full manual.

1. **Give it one job.** Diagnosis, durable intake, and repair have different evidence, permissions, and completion criteria, so they are separate skills.
2. **Say when it applies—and when it does not.** The description should route the right requests without attracting unrelated work.
3. **Name the required inputs.** Do not let the agent guess the repository, scraper identity, source of truth, work-record schema, or owner.
4. **Separate facts from hypotheses.** An alert is evidence of a symptom; the diagnosis must be checked against the live source, run output, code, and product.
5. **Make writes safe to repeat.** Before creating a work item, search for an active record with the same scraper and failure class. Update the existing record when it is the same incident.
6. **Put people at judgment points.** An engineer reviews the diagnosis, estimate, fix, and production result. The skill does not silently promote a draft into accepted work.
7. **Define observable outputs.** A good run leaves a diagnosis record, evidence links, a tested pull request, or a named follow-up—not “task completed.”
8. **Include stop conditions.** Missing access, uncertain source authority, sensitive credentials, unclear duplicates, or an untestable failure should trigger a handoff rather than a guess.

Keep source-specific facts in the spider, fixture, or work record. Keep mandatory invariants in tests and CI. Keep schedules, account setup, and connector configuration in their platform-specific configuration rather than presenting them as portable skill behavior.

## Copyable Skills

- [`diagnose-scraper-alert`](../skills/diagnose-scraper-alert/SKILL.md) turns a digest item or alert into an evidence-backed draft diagnosis and effort range for engineer review.
- [`record-scraper-diagnosis`](../skills/record-scraper-diagnosis/SKILL.md) saves an accepted diagnosis to Airtable or the configured tracker, updating an existing active incident instead of creating a duplicate.
- [`repair-scraper-issue`](../skills/repair-scraper-issue/SKILL.md) takes an approved work item through reproduction, the smallest safe fix, review, pull request, and production-validation handoff.

Copy the complete skill folder into the location supported by the chosen coding-agent product. Confirm current discovery and metadata rules in that product's documentation; do not assume that local and hosted agents load skills the same way.

## Improve the Skills Through Use

When a real task exposes a gap, update the smallest relevant instruction and explain the evidence in the pull request. Do not turn one scraper's behavior into a global rule without checking another source. Keep each change visible and reversible.
