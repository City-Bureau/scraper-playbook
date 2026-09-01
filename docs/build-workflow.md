# CtD Scraper Agent — Build Workflow

[Playbook home](../README.md) · [First 30 Minutes](first-30-minutes.md) · [Build](build-workflow.md) · [Repair](repair-workflow.md) · [Review](review-and-handoff.md) · [Learnings](reusable-learnings.md) · [Skills](workflow-skills.md) · [Templates](templates.md)

## Outcome

A build is implementation-ready when the expected meetings are complete, correct, current, traceable to a public source, and ready to move through the repository's normal review and deployment path. The task closes only after production delivery is confirmed or a named follow-up owns that confirmation. Generated code, a fixture, green tests, or a merged PR are intermediate outputs—not the user outcome.

This workflow is **proposed** for CtD. It draws on current City Scrapers conventions and one agent-assisted repair, but we do not yet have evidence from a completed CtD agent-assisted build.

## 1. Write the Scraper Contract

Before implementation, create a one-page contract using [Templates](templates.md). It should answer:

- Which public meeting body is in scope?
- Which source is authoritative for dates, times, cancellations, location, and documents?
- What date window should the spider return?
- Which meetings must be excluded?
- What does the source do when there are no meetings?
- What should the run do when the page or endpoint is malformed?
- How will the team know the output reached the correct agency downstream?

The contract is a shared reference for the engineer, agent, reviewer, and future repairer. It is not a replacement for tests.

## 2. Discover the Source With a Browser

Start from the public page a resident would use. Browser discovery may use a normal browser, developer tools, browser automation, screenshots, or an HTTP client depending on the environment. The goal is evidence, not a specific tool.

### Inspect the visible experience

- Identify the agency/body name displayed to users.
- Record several future and recent meetings, including cancellations or special meetings.
- Check pagination, “load more,” year filters, and calendar navigation.
- Note whether agenda, minutes, video, or remote-access links live on a detail page.
- Capture timezone and any source-specific date convention.

### Inspect how the page gets its data

- Does the initial HTML contain the meetings?
- Does the page call a public JSON, XML, RSS, iCalendar, Granicus, Legistar, BoardDocs, or other endpoint?
- Are identifiers or filters needed to isolate the correct body?
- Does a list endpoint require a second detail request?
- Does JavaScript rendering make browser automation necessary, or can the public endpoint be requested directly?

Prefer a stable public endpoint used by the site's own interface when it reduces brittle markup parsing. Do not assume an endpoint is stable merely because it is JSON. Record its public provenance and expected shape.

### Access boundaries

- Identify honestly with a project-appropriate user agent.
- Do not spoof a consumer browser to bypass controls.
- Do not store session cookies, authentication headers, or access tokens in fixtures or Git.
- If the source requires authentication, aggressive circumvention, or unclear terms, stop for a human decision.

## 3. Learn the Repository's House Style

Have the agent read two or three **current, similar** spiders and their tests in the same repository. Similar means same source platform or request shape—not simply the same city.

Ask explicitly:

- Is there an existing mixin or shared parser for this platform?
- Which spider is the best-maintained example rather than merely the closest name?
- What naming convention does the repository use today?
- Which CI and validation steps run on a changed spider?
- Does the repository have staging or a source-specific deployment rule?

Existing code is evidence, not automatically a model. Some local repositories contain stale fixtures, commented alternatives, synchronous calls inside callbacks, or older naming conventions. The reviewer should be able to explain why an example was chosen.

## 4. Scaffold, Then Inspect the Scaffold

Current City Scrapers Core provides a generator that can create a spider skeleton, test skeleton, and saved fixture from the source URL. Use the repository's documented generator when available so names and paths follow local conventions.

Treat generated files as a starting point:

- multi-page or list-plus-detail sources need additional design;
- generated test placeholders must be replaced with real assertions;
- the saved response must be checked for secrets, consent walls, or personal information before commit; and
- a spider name is part of meeting identity, so renaming a live spider can have downstream effects.

Do not hand-edit around a broken generator without recording why. Fixing shared scaffolding may help many repositories, but it has a larger blast radius and needs separate review.

## 5. Implement the Shared Meeting Contract

The spider should follow the repository's current `CityScrapersSpider` and `Meeting` conventions:

- stable spider name, human-readable agency, and correct timezone;
- source requests with explicit callbacks and bounded pagination;
- one `Meeting` item per in-scope public meeting;
- correct title, description, classification, start/end, all-day flag, location, links, and source;
- repository helpers for status and ID unless current local guidance says otherwise; and
- explicit filtering that does not silently discard an in-scope body.

Ask the agent to explain non-obvious transformations. A date parser, body filter, fallback location, or cancellation rule should be traceable to source evidence.

### Fail visibly

Decide how the spider should signal an unexpected empty or malformed source. A run that exits successfully with zero items can look healthy while delivering nothing. Schema validation alone may not catch that condition.

Do not turn every legitimate no-meeting period into an incident. The contract should distinguish an expected empty window from a source that stopped matching.

## 6. Build Deterministic Fixture Tests

Committed fixtures and frozen-clock tests make parser behavior reproducible. Tests should read like the scraper contract.

Cover:

- expected item count for the fixture;
- agency/body filtering;
- dates, local times, timezone behavior, and end-time absence;
- title and classification;
- cancellation/status behavior;
- location structure;
- agenda, minutes, video, and source links;
- stable ID behavior; and
- at least one awkward item, not only item zero.

Inspect generated tests. A placeholder or assertion that never references parsed output can pass forever. If the agent writes a helper or shared mixin, add direct tests for its boundaries and affected spiders.

## 7. Verify Complete, Correct, and Current

Run the repository's documented style, test, and scraper-validation gates, then run the spider against the live source. Commands differ by repository; follow current local guidance rather than copying a stale command block.

Compare live output with the ground-truth ledger:

### Complete

- Are all expected meetings in the date window present?
- Are special, cancelled, rescheduled, and multi-body meetings handled?
- Did pagination or a detail request silently stop?

### Correct

- Do title, body, date/time, status, location, links, and source match?
- Are day/month parsing and timezone assumptions explicit?
- Are meetings attached to the correct agency identity?

### Current

- Is the source live rather than only the saved fixture?
- Does output include the newest published meeting?
- Are corrections or cancellations reflected within the expected window?

Record the comparison; “looks good” is not reviewable evidence.

## 8. Review and Handoff

Use [Review and Handoff](review-and-handoff.md). The pull request or handoff should include:

- source and scope;
- the scraper contract;
- chosen repository examples and why;
- fixture date and any sanitization;
- test and live-run results;
- expected-versus-actual meeting evidence;
- known limitations and monitoring assumptions; and
- owner of post-deploy confirmation.

After deployment, confirm that meetings appear under the correct agency in the production database or public product. Then capture reusable evidence with [Reusable Learnings](reusable-learnings.md).

## Local Reference Artifacts — Verify Before Use

These local artifacts illustrate current patterns. They were inspected on 2026-08-31, when the Tulsa checkout was behind `origin/main`, the Indianapolis checkout was on `staging`, Fort Worth `main` matched `origin/main`, and installed/core versions differed across checkouts. Treat them as navigation aids, not pinned canonical examples; inspect the target repository's current ref before use.

| Reference | Useful for | Current caveat |
| --- | --- | --- |
| `city-scrapers-tulsa/city_scrapers/spiders/tulok_citycouncil.py` and `tests/test_tulok_citycouncil.py` | Granicus source, body filtering, and fixture assertions | Confirm the current remote branch before copying |
| `city-scrapers-tulsa/.github/workflows/ci.yml` and `.github/PULL_REQUEST_TEMPLATE.md` | CI gates and evidence-oriented handoff | Repository-specific, not universal policy |
| `city-scrapers-fortx/city_scrapers/spiders/fortx_Fort_Worth_City_Council.py` and its tests | List-plus-detail API and multi-request fixture pattern | Also demonstrates why date assumptions require adversarial review |
| `city-scrapers-indianapolis/city_scrapers/spiders/ind_school_board.py` | BoardDocs XML discovery | Dated fixture and fallback behavior should not be copied without review |
| `city-scrapers-core/docs/commands.rst`, `items.py`, `spiders/spider.py`, and `pipelines/validation.py` | Generator, `Meeting` schema, identity helpers, and validation behavior | Installed/core versions differ across checkouts; use the version in the target repo environment |

The important reusable pattern is not any single file. It is: scaffold → inspect live source → implement shared schema → fixture test → live crawl → source/output comparison → human review → production confirmation.
