# Scraper Playbook

Clear, practical guidance for Code the Dream engineers using coding agents to build and repair City Scrapers.

Code the Dream owns the work. Coding agents can help investigate, draft, test, and collect evidence, while CtD engineers own scope, review, merge, deployment, and production validation.

## Read the playbook

- [Orientation and shared workflow](docs/index.md)
- [First 30 Minutes](docs/first-30-minutes.md)
- [Build Workflow](docs/build-workflow.md)
- [Repair Workflow](docs/repair-workflow.md)
- [Review and Handoff](docs/review-and-handoff.md)
- [Reusable Learnings](docs/reusable-learnings.md)
- [Workflow Skills](docs/workflow-skills.md)
- [Copyable Templates](docs/templates.md)

## Copyable Skills

- [`diagnose-scraper-alert`](skills/diagnose-scraper-alert/SKILL.md): investigate an alert and draft a diagnosis and estimate for engineer review.
- [`record-scraper-diagnosis`](skills/record-scraper-diagnosis/SKILL.md): save an accepted diagnosis without duplicating the same active failure.
- [`repair-scraper-issue`](skills/repair-scraper-issue/SKILL.md): take an approved issue through reproduction, repair, review, pull request, and production-validation handoff.

See [Workflow Skills](docs/workflow-skills.md) for the design choices behind these examples and how routines, connectors, durable records, and skills fit together.

## Status

This is an initial playbook prepared for a CtD-owned pilot. Proposed guidance should be tested and revised through normal pull requests as the team completes genuinely new scraper work.

## Contributing

Code the Dream engineers can adapt and maintain this playbook as the work evolves. Open a focused pull request that explains what prompted the change, where it applies, and how reviewers can verify it. Repository-specific instructions remain the source of truth when they differ from this shared guidance.

## Safety

Do not commit credentials, tokens, cookies, personal data, raw private session transcripts, or internal repository details. Prefer public-source evidence and short case records with sensitive details removed.
