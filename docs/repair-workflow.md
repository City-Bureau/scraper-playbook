# CtD Scraper Agent — Repair Workflow

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Templates](templates.md)

## Outcome

A repair is complete when the original failure is reproduced and explained, the smallest safe change is reviewed, expected meetings are again complete/correct/current, and recovery is confirmed where users depend on the data.

The historical Wayne County incident informs this workflow but is not the model to replay. A fair CtD trial uses a genuinely unresolved repair.

## The Repair Standard

Every repair should leave evidence for six questions:

1. **Detection:** How was the failure surfaced, and who responded?
2. **Diagnosis:** Which boundary failed, and what evidence proves it?
3. **Safe implementation:** What is the smallest change, regression test, and blast radius?
4. **End-to-end verification:** Are meetings complete, correct, current, and attached to the right agency?
5. **Operational ownership:** Who reviews, deploys, confirms recovery, and watches for recurrence?
6. **Reusable learnings:** What should future work retrieve, and where can engineering control it?

## 1. Preserve the Failure Signal

Start from what was observed:

- monitoring or `EMPTY_RESULT` signal;
- exception or failed scheduled run;
- stale “last scraped” time;
- missing, duplicated, or incorrectly dated meetings;
- incorrect agency match;
- reporter or program-team observation; or
- a live source change discovered during another task.

Copy the exact message, source URL, observed time, and expected user outcome into a repair record. Do not rewrite the symptom into a diagnosis before investigating.

## 2. Reproduce Before Diagnosing

Compare four surfaces:

| Surface | Question |
| --- | --- |
| Live authoritative source | What meetings and fields exist now? |
| Current live spider output | What does the code return now? |
| Committed fixture and tests | What historical shape does the repository expect? |
| Ingestion/product output | Did valid output reach the right agency and user-facing surface? |

This separates common failure boundaries:

- selector or endpoint drift;
- pagination/listing failure;
- detail-page or document-link failure;
- date, time, timezone, or cancellation parsing;
- source blocking or access-policy change;
- shared mixin or core behavior;
- ingestion/schema rejection;
- agency-name or identifier mismatch; and
- monitoring/status logic that reports success despite no useful data.

Use browser inspection when the source is dynamic. Check rendered content and the page's own public network requests before deciding that browser automation is required in production.

## 3. Name the Failing Boundary

Require a diagnosis that points to code and evidence:

> The live source now returns `<observed shape>`. `<file:line or function>` expects `<old shape>`, causing `<measured output or failure>`. The affected scope is `<one spider / shared mixin / repository / downstream importer>`.

If the agent cannot name the boundary, it is not ready to patch.

Ask:

- What else calls this parser, mixin, helper, or endpoint?
- Are sibling spiders likely to share the failure?
- Could a “fix” hide the signal by swallowing an exception or weakening a test?
- Is the actual problem outside scraper code?

## 4. Prove the Regression Test Can Fail

Refresh or add the smallest safe fixture needed to represent the current source. Before applying the fix:

1. add the regression assertion;
2. run it against the broken implementation;
3. retain the failing result in the repair record; and
4. only then implement the change.

A test written after the patch and never seen red proves little. Also check that the test exercises the real entry point rather than a helper that still succeeds after the listing path breaks.

For an empty-result failure, test the intended signal. An unrelated exception or warning is not proof that the run fails usefully.

## 5. Make the Smallest Safe Change

Prefer a focused change that preserves repository conventions. Avoid opportunistic rewrites during incident repair unless the current structure prevents a safe fix.

The agent should state:

- files changed and why;
- source evidence for each changed rule;
- shared-code blast radius;
- behavior on malformed, empty, or partial input;
- what remains unresolved; and
- how to reverse the change.

Never “fix” a blocked source by committing private cookies, spoofed identities, or brittle circumvention. A valid outcome may be to contact the agency, use another public source, or explicitly mark the source unsupported.

## 6. Run Adversarial Review

The reviewer tries to disprove both the code and the tests:

- Can the new test be made green while the real path is broken?
- Does only the first meeting get asserted?
- Could the change drop a valid edge case or introduce a performance problem?
- Does a shared helper change more spiders than the PR claims?
- Are claims backed by the live source rather than copied from a ticket?
- Does the scraper fail visibly on the original failure shape?

Automated review can help, but a CtD engineer owns which findings are accepted. Verify reviewer claims against source evidence; reviewers can be wrong.

## 7. Verify and Validate End to End

After local gates pass:

- run the spider against the live source;
- compare expected and actual meeting sets and fields;
- confirm no new duplicate or missing items;
- verify affected siblings when shared code changed;
- deploy through the normal reviewed path; and
- confirm meetings appear under the correct agency in the production database or public product.

If the scraper feed is correct but the product is not, continue diagnosis downstream. “The spider works” and “the user outcome is restored” are different claims.

## 8. Close the Loop

Complete the repair record and handoff:

- original signal and detection time;
- cause and affected boundary;
- failing-then-passing test evidence;
- live source and output comparison;
- review findings and dispositions;
- deployment and production confirmation;
- owner and monitoring follow-up; and
- reusable learning candidate.

Use [Templates](templates.md) and [Reusable Learnings](reusable-learnings.md).

## Tests Are Not Monitoring

A regression test can prevent a known defect from returning when code changes. It cannot detect a city website redesign next month when nobody opens a pull request.

A reliable operating model still needs feed-level signals for unexpected silence, staleness, duplicates, implausible counts, or repeated errors—and a person or team accountable for responding.

## Stop and Escalate When

- the source of truth is ambiguous;
- the source requires credentials or questionable circumvention;
- the change affects shared infrastructure beyond the task;
- the environment cannot reproduce or test the failure;
- the repair would weaken validation or silence an error;
- source and product disagree but the relevant downstream system is unavailable; or
- the proposed behavior requires a product or editorial decision.
