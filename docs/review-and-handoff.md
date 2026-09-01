# CtD Scraper Agent — Review and Handoff

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Skills](workflow-skills.md) · [Templates](templates.md)

## Purpose

Review checks that agent-assisted work is safe and useful. The goal is not to approve a plausible diff; it is to determine whether the change restores or creates reliable meeting availability without hiding a new failure.

CtD owns the review and merge decision. PDW may help CtD improve tools, prompts, or shared guidance, but does not replace CtD as delivery owner.

## Roles

| Role | Owns |
| --- | --- |
| CtD task owner | Scope, source choice, judgment calls, acceptance, merge, and handoff |
| Coding agent | Bounded investigation, draft code/tests, tool execution, and evidence collection |
| CtD reviewer | Independent challenge of evidence, code, tests, and user outcome |
| PDW enablement | Help adapting agent practices or diagnosing workflow gaps inside CtD's process |
| Production-validation owner | Confirming meetings reach the correct production surface and recording recovery |

One person may hold several roles, but the author should not be the only reviewer of a meaningful change.

## Review in Five Layers

### 1. Source evidence

- Is the public source authoritative for this body and field?
- Do cited meetings exist at the cited URLs?
- Are date conventions, timezone, cancellations, and body filters grounded in evidence?
- Were numbers and ticket references checked at their source rather than repeated from a summary?

### 2. User-visible behavior

- Are expected meetings complete, correct, and current?
- Are they attached to the right agency?
- Are agenda, minutes, video, remote-access, and location details usable?
- What happens when the source is empty, partial, malformed, or redesigned?

### 3. Tests

- Was a repair test shown failing before the fix?
- Does the test call the real entry path?
- Can the test pass without asserting parsed output?
- Does it cover more than the easiest or first meeting?
- Do damaged or empty inputs fail visibly for the right reason?
- If shared code changed, are affected siblings exercised?

### 4. Implementation

- Is the change the smallest safe one?
- Does it match current repository conventions and schema helpers?
- Are pagination, callbacks, and detail requests bounded?
- Did synchronous or browser-driven behavior enter a normal Scrapy path without justification?
- Could the change create a performance or scope regression?

### 5. Operations

- Who detects a future break?
- Who receives the signal and owns response?
- What must be checked after deployment?
- What evidence and code remain if a tool or service disappears?
- What learning should the next task retrieve?

## Adversarial Review

Ask a reviewer—human, agent, or both—to try to disprove the change.

Useful review prompt:

> Review this scraper change as an adversary. Check the cited live source before accepting any claim. Try to find a valid meeting the code drops, an out-of-scope meeting it includes, a date/status/location/link it misreads, a malformed or empty response it treats as success, a test that cannot fail, and any shared-code or performance impact. Separate confirmed findings from hypotheses.

Automated reviewers are assistants, not authorities. In the source incident, reviewers found real blocking defects, but some findings were also wrong and were discarded after live verification.

## Findings Need Dispositions

For each review finding, record:

- finding and severity;
- evidence checked;
- confirmed, rejected, or deferred;
- resulting change or reason for no change; and
- owner of any follow-up.

Do not apply a finding merely because several agents repeat it. They may share the same mistaken assumption.

## Shared `SKILL.md` Guidance

A `SKILL.md` can make a repeatable workflow discoverable to humans and agents. Treat it as reviewed operational guidance.

See [Workflow Skills](workflow-skills.md) for a worked example and the copyable diagnosis and repair skills.

### Put in a shared skill

- when the workflow applies;
- required inputs and evidence;
- the stable sequence of checks;
- human approval and stop points;
- outputs and handoff requirements;
- links to repository-specific guidance; and
- how changes are reviewed and reversed.

### Keep elsewhere

- mandatory invariants that can be enforced by tests or CI;
- source-specific facts that belong in a spider, fixture, or learning record;
- long incident narratives better kept as case records; and
- secrets, credentials, raw private logs, or personal data.

### Governance

- Keep skills small enough to review.
- Require a normal pull request and named owner.
- Label platform-specific adapters.
- Record why the guidance changed and which case supports it.
- Allow engineering to disable or revert a skill without changing application code.
- Re-test the workflow after major repository or agent-platform changes.

A skill is not model training and should not silently change itself. A proposed improvement becomes shared guidance only through the team's visible review process.

## Pull Request and Handoff Package

Use the template in [Templates](templates.md). At minimum, include:

- user problem and task boundary;
- authoritative source and evidence ledger;
- files changed and why;
- fixture date and sanitization note;
- test, lint, validation, and live-crawl results;
- expected-versus-actual meeting comparison;
- adversarial findings and dispositions;
- known limitations and unverified assumptions;
- deploy and production-validation owner; and
- learning candidates.

## Definition of Done

- [ ] The source and scope are explicit.
- [ ] Tests and live-source checks pass for the intended reason.
- [ ] Complete/correct/current output is demonstrated.
- [ ] Agency matching or downstream delivery has a validation plan.
- [ ] A person reviewed the change and findings.
- [ ] Shared-code impact is understood.
- [ ] Monitoring and response ownership are named.
- [ ] Remaining limits are written plainly.
- [ ] Reusable learnings are captured as reviewable candidates.

The change can merge before production validation, but the task is not closed until the user-visible outcome is confirmed or a named follow-up owns that check.
