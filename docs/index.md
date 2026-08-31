# Code the Dream Scraper-Agent Cookbook

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Templates](templates.md)

## Start Here

This is a shared guide for Code the Dream (CtD) engineers using coding agents to build and repair City Scrapers. People and coding agents can use it, and the team can update it through normal pull requests.

**Ownership:** CtD owns scraper builds, repairs, review decisions, and handoff. Public Data Works (PDW) can help CtD adopt and improve agent-assisted practices when useful. That support stays within CtD's workflow rather than moving delivery to a separate PDW team.

To start a work session, open [First 30 Minutes](first-30-minutes.md).

## What This Playbook Covers

- Turn a meeting-data need into a reviewable scraper change.
- Use an agent for repeatable tasks while engineers keep decision-making responsibility.
- Check the user outcome: complete, correct, current meetings attached to the right agency.
- Make empty or stale results visible even when a run reports success.
- Preserve useful learnings so the next task starts with relevant evidence.

This playbook does **not** promise that agents make scraper work faster. We have evidence from one completed agent-assisted repair, but not from a CtD Scrapy build and not enough data to compare speed or cost. Treat the guidance as a starting point to test and improve through CtD's work.

## Choose Your Path

| If you need to… | Go to… | Finish with… |
| --- | --- | --- |
| Start safely and understand the workflow | [First 30 Minutes](first-30-minutes.md) | A clearly scoped task, working environment, and written source-of-truth plan |
| Build a new spider | [Build Workflow](build-workflow.md) | A live-checked spider, fixture tests, validation evidence, and draft PR |
| Diagnose or repair a spider | [Repair Workflow](repair-workflow.md) | Reproduced failure, smallest safe fix, red-then-green regression test, and production validation plan |
| Review or hand work to another person | [Review and Handoff](review-and-handoff.md) | A challenging review and an evidence-rich handoff |
| Capture something the next task should reuse | [Reusable Learnings](reusable-learnings.md) | A source-linked, reviewable learning that engineering controls |
| Copy a checklist or record | [Templates](templates.md) | A scraper contract, repair record, learning record, or handoff template |

## The Shared Workflow

The same loop applies to builds and repairs:

> scope → inspect → reproduce or establish ground truth → implement → review → verify → deploy → validate → capture learnings

Three distinctions matter:

1. **Tests versus monitoring:** tests run when code changes; monitoring detects a source that breaks later.
2. **Verify versus validate:** verify claims against live source evidence; validate that the meeting reaches the production database or public product.
3. **Agent output versus ownership:** an agent can draft code and evidence; a CtD engineer owns the decision to accept, change, merge, deploy, and report it.

## Evidence Labels

Use these labels when adding guidance:

- **Verified:** observed in current code, a live source, a completed incident, CI, or production output.
- **Proposed:** a workflow choice to test with CtD.
- **Platform-specific:** depends on the coding-agent product or execution environment and must be confirmed there.
- **Unknown:** important but not yet established.

Do not let a proposed practice become a “fact” because it was copied into several files.

## Safety Defaults

- Keep people at the merge, deploy, and production-change gates.
- Use read-only production access for diagnosis; ship changes through reviewed code.
- Never paste credentials, private tokens, cookies, personal data, or raw private session logs into Git.
- Identify the scraper honestly. Do not spoof browser identity or replay captured session cookies.
- Prefer public source material and the site's own stable endpoint when appropriate.
- Treat reviewer findings as claims to verify, not instructions to apply automatically.
- Stop when the environment cannot run the relevant checks; an agent that cannot verify is likely to guess.

## Local and Web-Hosted Agent Workflows

The workflow is portable; product features are not.

**Verified common needs:** access to the repository and its history, a writable task branch, the repository's dependency environment, a way to inspect the public source, the relevant tests and validators, and a normal pull-request path.

**Confirm for each platform:** whether work persists between sessions; whether shell, browser, or HTTP tools are available; how secrets are supplied; whether the agent can create branches or PRs; whether CI results are visible; and whether a session can be exported. Do not assume a hosted interface supports a feature because a local tool does, or vice versa.

If a capability is missing, keep the workflow intact and make the handoff explicit. For example, an agent can prepare a patch and validation plan while a CtD engineer runs the live crawl or opens the PR.

## How This Cookbook Changes

Small improvements are welcome. A change should say:

- what task or failure motivated it;
- what evidence supports it;
- whether it is global, repository-specific, or source-specific;
- who reviewed it; and
- how to reverse or disable it if it causes trouble.

Shared `SKILL.md` guidance belongs here only after review. It is operational instruction—not unreviewed training data and not a dumping ground for case histories.

## Evidence Boundary

This cookbook synthesizes five August 2026 research briefs and review of the City Scrapers framework and working conventions available during drafting. A historical repair incident contributes failure patterns and review learnings; it is not a task to replay or evidence that CtD has already used this workflow.

Guidance labeled **proposed** should be tested on genuinely new CtD work. When the cookbook and a current repository disagree, the repository's reviewed instructions and code are the source of truth.

## Contributing

This is a living playbook. Improve it through small, reviewable pull requests tied to evidence from real builds and repairs. Code the Dream should name the reviewer who decides which proposed practices become shared guidance.
