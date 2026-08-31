# CtD Scraper Agent — Reusable Learnings

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Templates](templates.md)

## Purpose

Every build or repair should make the next relevant task easier without turning one source-specific incident into a universal rule. The learning system uses a visible, reviewable loop:

> capture → review → make available → retrieve → verify in the new context → correct or retire

This is not autonomous self-training. A prompt, context window, session transcript, or model memory is not durable organizational learning by itself.

## What to Capture

A reusable learning should contain:

- a concise statement of what was learned;
- source, repository, framework, and failure-shape scope;
- the source evidence or failure signal;
- diagnosis and code boundary;
- change made;
- validation result, including production outcome when available;
- owner and reviewer;
- links to ticket, pull request, tests, and public source;
- status and version history; and
- limits, counterexamples, or expiry/review date.

Capture the reasoning needed to reuse the pattern, not a full replay of the session.

## Candidate First

New learnings begin as reviewable candidates. A candidate can be useful without being universally available.

Suggested states:

| State | Meaning | Future work uses it? |
| --- | --- | --- |
| Candidate | Captured, not yet reviewed | Only when explicitly requested |
| Available | Reviewed for a stated scope | Yes, as a hypothesis to verify |
| Hidden | Kept for audit but omitted from normal retrieval | No |
| Disabled | Temporarily unavailable while being investigated | No |
| Retired | Superseded or no longer applicable | No; replacement is linked |
| Removed | Deleted under an approved policy | No; deletion receipt remains where appropriate |

Automatic promotion may eventually be appropriate for narrowly defined cases with measured quality, but it is not supported by the current scraper evidence and should not be assumed.

## Retrieve Before New Work

Before a build or repair, retrieve learnings using concrete context:

- source platform, such as Granicus, Legistar, BoardDocs, or a city calendar API;
- repository and shared mixins;
- failure signal, such as silence, duplicates, wrong dates, or agency mismatch;
- affected fields and date window; and
- task type: build, repair, review, monitoring, or downstream validation.

The engineer and agent should see the learning's scope, evidence, status, and provenance—not only its recommendation.

Retrieved learnings are starting hypotheses. Verify them against the current live source and current code before applying them.

## Cross-Repository Learnings

Scope should be explicit:

- **Source-specific:** one agency or endpoint.
- **Repository-specific:** naming, CI, fixtures, or deployment behavior in one city repo.
- **Platform pattern:** a public meeting system used by several agencies.
- **Framework-wide:** `CityScrapersSpider`, `Meeting`, or shared core behavior.
- **Operating practice:** review, handoff, privacy, or validation guidance.

Promote a source-specific observation to a broader scope only after it has been verified in another context. Link the cases that justify the broader pattern.

## Engineering Controls

Engineering must be able to see where learnings live and change their effect without deploying scraper application code or restarting services.

At minimum, the chosen store should support:

- inspect and search;
- edit with version history;
- hide or temporarily disable;
- restore a prior version;
- retire or remove under policy;
- scope which repositories or tasks retrieve a learning;
- see who changed status, when, and why; and
- audit which learning was presented during a task.

A live database-backed record set, repository-backed knowledge index, or equivalent durable store could satisfy this model. This cookbook deliberately does not choose the technology stack.

## What Belongs in Git

Good Git artifacts:

- reviewed `SKILL.md` workflow guidance;
- public-source case summaries;
- scraper contracts and repair records without sensitive data;
- links to tickets, PRs, fixtures, tests, and validation evidence; and
- changes to shared checklists or templates.

Do not commit:

- credentials, tokens, cookies, or private headers;
- private personal information;
- copied customer or partner data without authorization;
- raw private session transcripts;
- unredacted terminal logs containing environment details; or
- confidential source material merely because an agent saw it.

## Optional Session and Case Capture

Session capture is optional. The durable unit should usually be a short case record, not a raw transcript.

Record only what improves reproducibility:

- task and source;
- decisions and alternatives considered;
- important evidence;
- commands or tools only when their result matters;
- tests and validation outcome;
- review findings; and
- resulting learning candidates.

Before sharing, remove secrets, personal data, irrelevant internal paths, copied private content, and speculative commentary. Link to access-controlled systems rather than duplicating their contents.

Do not claim a local or hosted agent can export sessions unless that capability has been verified from authoritative current documentation. The workflow works without session export.

## Correcting a Bad Learning

When a learning is wrong or too broad:

1. disable it from normal retrieval;
2. preserve its history and affected scope;
3. record the counterevidence;
4. correct, narrow, retire, or remove it;
5. link a replacement if one exists; and
6. check whether recent work relied on it.

Corrections are valuable evidence. Do not hide them by silently rewriting history.

## Success Measures

Measure the learning system by outcomes, not record count:

- relevant prior evidence retrieved before work;
- fewer repeated investigations;
- faster diagnosis without more review defects;
- percentage of used learnings with visible provenance;
- corrections made promptly and reversibly;
- stale or over-broad guidance retired; and
- CtD engineers reporting that retrieval helps rather than distracts.

## Open Design Decisions

- Which durable store should be the operational source of learnings?
- Who reviews candidates and changes availability?
- Which learnings apply globally, by repository, or by source?
- What retention and deletion rules apply?
- How are learnings presented inside local and hosted agent workflows?
- Which state changes require one reviewer versus two?

These choices should follow a small CtD-owned pilot, not precede it with a large platform build.
