# CtD Scraper Agent — First 30 Minutes

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Templates](templates.md)

## The Goal

The goal is not to produce a patch immediately. By minute 30, you should have a clearly scoped task, a working environment, a clear source of truth, and a written plan another person can review.

## Minutes 0–5: Name the User Outcome

Write down:

- the agency and public meeting body;
- whether this is a new build or a repair;
- the authoritative public source URL or URLs;
- what a correct result means for a person using Documenters.org; and
- who owns review, merge, deployment, and production confirmation.

For a repair, include the observed symptom exactly as reported. “The scraper is broken” is not enough; “the source lists four future meetings, but Documenters.org lists none” is actionable.

## Minutes 5–10: Confirm the Working Environment

Check capabilities instead of assuming them.

- Is this the correct repository and task branch?
- Can the project dependencies install or run as documented?
- Can you run the existing test suite and the target spider?
- Can you inspect the live public source with a browser or HTTP tool?
- Can you read CI and open or update a pull request?
- Are production credentials unnecessary for the task? They usually should be.

If a required capability is missing, record the handoff rather than asking the agent to improvise around it.

### Local workflow

A local agent commonly works in an existing checkout or worktree and can use the repository's own shell tools. Confirm branch state and preserve unrelated changes. Do not assume the agent may install system packages, access a GUI browser, or use stored credentials.

### Web-hosted workflow

A hosted agent may use an isolated checkout with different persistence, browser, secret, or PR behavior. Confirm those features in the authoritative product documentation or the live interface. If they are unavailable, split the work: the agent prepares evidence and code; a CtD engineer performs the missing local or authenticated step.

## Minutes 10–15: Read Before Asking the Agent to Write

Give the agent a short reading route:

1. repository guidance such as `AGENTS.md`, `CONTRIBUTING.md`, or reviewed `SKILL.md` files;
2. the target spider and test, if repairing;
3. two or three similar current spiders in the same repository;
4. the `Meeting` schema and shared helpers used by those spiders; and
5. the current CI workflow or contributor checklist.

The repository is a stronger specification than a long prompt. If examples disagree, stop and ask which convention is current.

## Minutes 15–20: Establish Ground Truth

Use the public source to write a tiny expected-meetings ledger. Capture enough variation to expose mistakes:

| Source evidence | Expected value | Why it matters |
| --- | --- | --- |
| Meeting title and body | Exact agency/body | Prevents cross-agency contamination |
| Start date and local time | Parsed datetime and timezone | Catches day/month and timezone errors |
| Status or cancellation | Expected status | Prevents cancelled meetings appearing active |
| Location or remote details | Expected structured value | Supports attendance |
| Agenda/minutes/source links | Public URL and label | Preserves provenance |

For a repair, compare the live source, current spider output, committed fixture, and downstream product. Do not diagnose from the fixture alone.

## Minutes 20–25: Agree on the Boundaries

Tell the agent:

- what files it may change;
- what must remain unchanged;
- which live systems are read-only;
- which checks must pass;
- what evidence must appear in the handoff; and
- what conditions require stopping for a person.

Useful stop conditions include unclear source authority, authentication or bot-protection questions, a shared mixin with an unknown blast radius, missing dependencies, incompatible source records, or a proposed change outside the task.

## Minutes 25–30: Approve a Short Plan

The plan should name:

1. the evidence to inspect;
2. the expected code and test changes;
3. the live and fixture checks;
4. the likely blast radius;
5. the review and handoff point; and
6. the production validation owner.

For a repair, require the cause in `file:line` terms and require the regression test to be shown failing before the fix. For a build, require a scraper contract before implementation.

## Copyable Opening Prompt

> We are working in the existing City Scrapers repository. CtD owns this task and the merge decision. First read the repository guidance, the target or similar spiders, their tests, and CI. Inspect the public source and write a short ground-truth ledger. Do not change code until you can state the task boundary, source authority, likely files, checks, and stop conditions. Never use or copy private credentials, cookies, or raw private session logs. Separate verified facts from assumptions.

## Ready to Continue When

- [ ] The agency, source, and user outcome are clear.
- [ ] The task is genuinely new work, not a replay with a known answer.
- [ ] The environment can run the relevant checks, or a human handoff is named.
- [ ] Existing repository examples and guidance have been read.
- [ ] Ground truth includes more than one easy meeting.
- [ ] Change boundaries and stop conditions are written.
- [ ] A CtD reviewer and production-validation owner are named.

Next: [Build Workflow](build-workflow.md) or [Repair Workflow](repair-workflow.md).
