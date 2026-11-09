# Contribution: [Calendar Core] Add Calendar Event Update Endpoint #23

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Riya Gandhi
**GitHub Username:** riyag0
**Issue:** https://github.com/NITRR-Official/CampusOS/issues/23
**Pull Request:** https://github.com/NITRR-Official/CampusOS/pull/134


One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built and refined issue-scout to find and evaluate open source issues that fit my skills**

I configured issue-scout with my fit profile, a GitHub search strategy, and ranking rules, then used it to scan and grade potential issues. The initial scan over prioritized very new issues from the same repository because my ranking favored low comment counts and recent updates. I updated the strategy to keep at most one issue from the same repository, then manually reviewed newer issues and used the scout to grade my final two choices, both of which received an accept verdict.

**Unit 6: Added voice-guard protection and local repository memory for CampusOS**

I installed the voice-guard PreToolUse hook to check GitHub comment commands before they are sent and verified that the hook was wired correctly using a harmless gh issue comment --help command. I also created a local CLAUDE.local.md file for CampusOS that records the repository's contribution rules, build and test commands, and the calendar backend architecture I found during a scoped orientation. The initial orientation only showed that feature APIs were loaded through plugins, so I inspected the calendar plugin and updated the memory with the exact route, controller, service, repository, schema, and test locations. I kept CLAUDE.local.md out of the contribution using .git/info/exclude and confirmed this worked because git status --short remained empty.


**Unit 7: Built and tested the CampusOS calendar update endpoint and used ship-gate to prepare the contribution for a PR**

I created a ship manifest with the repository's required test, lint, type check, and build commands and used those checks on my contribution branch. The checks confirmed that the calendar tests passed 115/115 along with the repository tests, lint, type check, and build. The ship-gate hook did not trigger correctly through Claude Code, so I switched to running the ship-gate manually before opening the PR. I also documented the repository's existing formatting failures and verified the nine files changed by my implementation separately with Prettier.

**Unit 8: Monitored my pull request, responded to maintainer feedback, and re-requested review**

I configured the PR monitor and created a playbook with response rules, staleness thresholds, nudge etiquette, and walk away criteria based on the CampusOS contribution guidelines and recent contributor PR activity. The monitor detected the maintainer's requested changes and later generated a draft response after I implemented, tested, and pushed the fixes. I rewrote the draft in my own words, verified that commit c49419a was the PR head, posted the response through Claude Code, and re-requested review. The monitor had Windows encoding and Claude authentication issues, so I enabled Python UTF-8 mode and reran it successfully.

---

## Why I Chose This Issue

I searched for good first issues that matched my experience with backend development, APIs, JavaScript/TypeScript, and databases. My issue-scout scan surfaced several possible issues, and I also manually reviewed issues to make sure they were still available and appropriate for a first contribution. I chose CampusOS #23 because it involves adding a backend PATCH endpoint for updating calendar events while preserving validation, authorization, and the existing controller structure. My issue-scout gave the issue an accept verdict with moderate difficulty. It fits my experience with REST APIs and backend development while giving me an opportunity to learn how to work within an unfamiliar open source backend and follow its existing architecture and conventions.

The issue-scout helped me evaluate whether issues matched my skills and had a manageable scope, but the search results did not always show whether an issue was actually still available. Some open issues I reviewed already had contributors working on them or had work that was effectively completed. Because of this, I learned that I still needed to manually check the full issue activity before choosing an issue. During Unit 6, I also updated the scout's scope rubric so that bounded issues with some open edges are treated as difficulty signals instead of being automatically rejected.

Claim comment: https://github.com/NITRR-Official/CampusOS/issues/23#issuecomment-6388620807


**Toolkit**

- Tool: issue-scout, using my fit profile, GitHub search strategy, and scope rubric to scan and grade candidate issues
- What it produced: The scout graded CampusOS #23 as accept with moderate difficulty and identified it as a good match for my backend and API experience
- Difficulties: The scan did not always show whether an open issue was actually still available, and some issues I reviewed already had contributors working on them or work that was effectively completed 
- What changed: I manually checked the full GitHub issue activity before choosing an issue and updated the scout's scope rubric so that bounded uncertainty affects the difficulty rating instead of automatically rejecting an issue


---

## Understanding the Issue

**Problem Description**

CampusOS currently does not provide an API endpoint for updating an existing calendar event. The repository layer already supports partial event updates through updateEvent(id, changes), but that functionality is not exposed through the service, controller, validation schema, or routes

**Expected Behavior**

An authorized user should be able to send a partial or full update to PATCH /api/v1/calendar/:eventId. The endpoint should allow supported calendar fields such as the title, event type, dates, description, and linked references to be updated while preserving the existing validation and authorization rules. Invalid updates should not be accepted and a request for an event that does not exist should return a 404 response.

**Current Behavior**

registerCalendarRoutes currently registers GET, POST, and DELETE operations but does not register a PATCH route. createCalendarController does not expose an update handler, CalendarService does not provide an update operation and a calendar.schema.js does not contain a schema for validating partial updates. As a result, the existing repository update functionality cannot currently be reached through the calendar API.

**Affected Components**

- plugins/calendar/backend/src/routes/calendar.routes.js - registerCalendarRoutes needs to register the PATCH endpoint using the existing calendar:manage permission
- plugins/calendar/backend/src/controller/calendar.controller.js -
createCalendarController needs an update handler that validates the request, calls the service, handles a missing event, and returns the updated event
- plugins/calendar/backend/src/service/calendar.service.js - CalendarService needs to expose the update operation and coordinate any validation that requires the existing event state
- plugins/calendar/backend/src/schema/calendar.schema.js - needs validation for partial calendar event updates while preserving the existing field and date rules
- plugins/calendar/backend/src/repository/calendar-event.repository.js and mongo-calendar-event.repository.js - already provide updateEvent(id,changes), so the existing repository update path can be reused rather than replaced
- plugins/calendar/backend/src/controller/calendar.controller.test.js and related calendar tests - need coverage for successful updates, partial updates, validation failures, 404 behavior, persistence, and authorization


**Toolkit**

- Tool: Manual code tracing, used to inspect the calendar route, controller, service, schema, repository, MongoDB repository, and existing controller tests
- What it produced: I traced the missing update path from the API route down to the persistence layer and found that updateEvent(id,changes) already exists in the repository while the route, controller, service, and update validation are missing
- Difficulties: The repository already contained update support and additional fields intended for future calendar features, so I needed to distinguish what was already implemented from what issue #23 actually requires
- What changed: I narrowed the planned work to exposing the existing repository update capability through the current calendar architecture and keeping the implementation limited to the fields and behavior required by issue #23


---

## Reproduction Process

**Environment Setup**

- OS: Windows 11
- Repository: NITRR-Official/CampusOS
- Branch: feature/23-calendar-event-update
- Repository commit: 42634891f02a6538043d15cfbf97845a25a94aa3
- Node.js: v24.21.0
- pnpm: 10.25.0 through Corepack
- Dependencies installed from the repository root with `corepack pnpm install`

I used Corepack to run the repository's configured pnpm version because `pnpm` was not directly available on my PATH. The install completed successfully. I also ran corepack pnpm test from plugins/calendar. The test command started the plugin's vitest run script, but failed because vitest was not recognized as a command. I therefore reproduced the missing feature by tracing the current calendar API registration and its controller, service, validation, and repository layers.

**Steps to Reproduce**

1. Open `plugins/calendar/backend/src/routes/calendar.routes.js`
2. Review the registered calendar routes. The file registers GET routes for listing, range queries, and individual events, a POST route for creating events, and a DELETE route for deleting events
3. Check for the endpoint requested by issue #23: `PATCH /api/v1/calendar/:eventId`
4. Open `plugins/calendar/backend/src/controller/calendar.controller.js` and review the exported handlers
5. Open `plugins/calendar/backend/src/service/calendar.service.js` and review the available calendar service operations
6. Open `plugins/calendar/backend/src/schema/calendar.schema.js` and review the request validation schemas
7. Open `plugins/calendar/backend/src/repository/calendar-event.repository.js` and compare the repository contract with the higher API layers

**Reproduction Evidence**

The requested `PATCH /api/v1/calendar/:eventId` endpoint is not currently registered in `calendar.routes.js`.

```javascript
export function registerCalendarRoutes(
  app,
  calendarController,
  requirePermissions
) {
  const manageCalendar = requirePermissions('calendar:manage');

  app.get('/api/v1/calendar', calendarController.list);
  app.get('/api/v1/calendar/range', calendarController.queryByRange);
  app.get('/api/v1/calendar/:eventId', calendarController.getById);
  app.post('/api/v1/calendar', manageCalendar, calendarController.create);
  app.delete(
    '/api/v1/calendar/:eventId',
    manageCalendar,
    calendarController.deleteEvent
  );
}

export default registerCalendarRoutes;
```

The controller exposes create, list, range query, get-by-ID, and delete handlers, but no update handler. The service similarly has no update operation, and the schema file contains create and range query validation but no update schema.

The repository layer already defines an `updateEvent(id, changes)` contract and notes that it exists to support future event editing for issue #23. This shows that update support has been prepared at the persistence layer, but it is not yet exposed through the service, controller, validation, or API route.

```javascript

 /**
   * Apply partial changes to an existing event.
   *
   * Only the fields present in `changes` are modified; omitted fields are left
   * unchanged. This method is part of the repository contract to support future
   * event editing (forward-looking for issue #23) even though the current
   * service does not yet expose an update operation.
   *
   * @abstract
   * @param {string} id The domain identifier of the event to update.
   * @param {UpdateCalendarEventChanges} changes Partial set of fields to apply.
   * @returns {Promise<CalendarEvent|null>} Resolves with the updated event as a
   *   normalized domain object, or `null` when no event has the given id.
   */
```

Expected behavior: an authorized user should be able to send a partial or full update through `PATCH /api/v1/calendar/:eventId`, with the existing validation and authorization rules preserved

Observed behavior: no PATCH route or corresponding controller/service/update-validation path currently exists, so the update endpoint described in issue #23 is not available

Reproduction commit: 42634891f02a6538043d15cfbf97845a25a94aa3

**Toolkit**

- Tool: repro-check, used to grade my claim comment and reproduction report against CampusOS issue #23
- What it produced: The final check returned an accept verdict with all five reproduction checks passing
- Difficulties: My first reproduction report did not include direct code evidence, and a later check found that I had not identified the exact repository commit used for reproduction
- What changed: I added excerpts from the calendar route and repository files as evidence, recorded the exact commit I reproduced against, and revised the test description to state only what I directly observed

---

## Solution Approach

**Analysis**

The issue is caused by a missing connection between the existing repository update functionality and the calendar API. CalendarEventRepository already defines updateEvent(id,changes) and MongoCalendarEventRepository implements it using findByIdAndUpdate, but CalendarService does not expose an update method. createCalendarController therefore has no update handler, calendar.schema.js has no schema for validating partial updates and registerCalendarRoutes has no PATCH route.

I confirmed this by tracing the current calendar backend implementation. registerCalendarRoutes contains GET, POST, and DELETE routes but no PATCH route. createCalendarController has no update handler, while the repository contract and MongoDB repository already contain updateEvent(id,changes). This shows that the persistence operation exists but is not currently connected to the API.

Partial date updates also need special handling. If a request changes only startsAt or only endsAt, validating only the request body is not enough to determine whether the resulting event has a valid date range. The update flow needs to preserve the existing date-range rule while allowing fields that were not included in the PATCH request to remain unchanged.


**Proposed Solution**

Add the missing update path while following the existing calendar backend architecture. I will add an update validation schema in calendar.schema.js, expose an updateEvent operation through CalendarService, add an update handler to createCalendarController, and register PATCH /api/v1/calendar/:eventId in registerCalendarRoutes using the existing calendar:manage permission.

The update should support partial requests, preserve the existing field and date validation rules, return a 404 when the event does not exist, and use the existing repository updateEvent implementation for persistence. I will not replace the repository implementation, change the database model, or add unrelated future calendar features such as recurrence or team assignment.


**Implementation Plan**

1. Modify plugins/calendar/backend/src/schema/calendar.schema.js to add a schema for partial event updates using the existing validation rules, including validation for supported fields and date values
2. Modify plugins/calendar/backend/src/service/calendar.service.js, controller/calendar.controller.js and routes/calendar.routes.js to connect
the existing repository updateEvent operation to PATCH /api/v1/calendar/:eventId, preserve date-range validation for partial updates, return 404 for missing events, and protect the route with calendar:manage
3. Update plugins/calendar/backend/src/controller/calendar.controller.test.js and the related calendar service tests to cover successful and partial updates, invalid input and date ranges, nonexistent events, persistence, and authorization. Run the calendar tests with corepack pnpm -r run test. The update tests should pass and the existing calendar test suite should continue to pass without regressions

**Unknowns/Risks**

The exact handling for date validation still needs to be confirmed during implementation because a partial update may provide only one date while the other date already exists on the stored event. I also need to confirm how malformed event IDs are currently handled so that the update endpoint follows the project's existing error behavior instead of assuming every missing or invalid ID should be handled the same way. The maintainer also mentioned PR #116 in the issue thread, but it does not currently appear to change the calendar files involved in this implementation.

No deviations yet. This plan will be updated if the implementation needs to change after plan-check or while building the fix.


**Toolkit**

- Tool: plan-check, used to review my implementation plan against the issue requirements, repository structure, and testing expectations
- What it produced: It reviewed my plan and identified missing evidence, a more specific testing plan, and unknowns that needed to be documented before implementation
- Difficulties: My first plan-check was rejected because the plan did not include enough evidence for the diagnosis, specific test files and commands, or the remaining risks around partial date updates and malformed event IDs
- What changed: I added code tracing evidence to the analysis, made the testing plan more specific with test files, commands, and expected results, and documented the remaining risks. After these changes, plan-check accepted the plan


---

## Testing Strategy

I tested the fix at both the focused calendar plugin and across the repository. Before the fix, I checked out the reproduction commit 42634891f02a6538043d15cfbf97845a25a94aa3 in a separate worktree and ran the calendar test suite. All 93 existing tests passed which confirmed the baseline before the update endpoint was added.

After implementing the fix, I ran corepack pnpm --filter @campusos/plugin-calendar test. All 6 test files and 115 tests passed. The new tests cover successful partial updates, persistence, invalid date ranges, clearing endsAt, empty or unsupported update fields, missing events, authorization, and service to repository behavior.

I also ran the repository wide test suite with corepack pnpm -r run test, which passed without a recursive test failure. I ran the repository lint checks which completed with no errors and one pre existing frontend warning, the frontend TypeScript check with corepack pnpm -r --filter frontend run type-check and the frontend build with corepack pnpm -r --filter frontend run build. Both completed successfully. git diff --check HEAD^ HEAD also returned no output which confirmed that there were no whitespace errors.

The repository wide formatting check has 632 pre existing formatting failures unrelated to issue #23, so I did not use it as evidence that this change introduced a formatting problem. Instead, I ran Prettier against the nine files changed by my implementation and all nine passed the formatting check.


**Toolkit**

- Tool: ship-gate manifest and repository test commands which was used to verify the implementation against the focused calendar tests and the repository's required checks
- What it produced: The calendar suite passed 115/115 tests after the fix compared with 93/93 at the baseline commit and the repository tests, lint, type check, build, whitespace check, and changed file formatting checks passed  
- Difficulties: The repository wide formatting check reports 632 existing formatting failures unrelated to my change and the repository's root test wrapper initially had a pnpm PATH issue on Windows
- What changed: I documented the repository wide formatting failure as a baseline condition, verified formatting only on the nine files changed by the fix and used Corepack to run the repository's configured pnpm version

---

## Implementation Notes

2026-10-31

I implemented PATCH /api/v1/calendar/:eventId using the existing calendar route, controller, service, and repository architecture. I added a partial update validation schema, an update handler in the controller, an updateEvent service method, and registered the PATCH route with the existing calendar:manage permission. I reused the repository's existing updateEvent implementation instead of adding new database logic.

For date updates, I handled the risk identified in my implementation plan by validating the final event state. When only startsAt or endsAt is provided, the service retrieves the existing event and validates the new date against the stored counterpart while still rejecting an invalid resulting date range. The existing 404 behavior is also preserved when an event cannot be found.

I added tests for partial updates, persistence, invalid date ranges, missing events, authorization, clearing endsAt, validation failures, and service to repository behavior. I also updated the existing service method exposure test from five methods to six so that it includes the new updateEvent method.

The implementation stayed within the accepted plan. I made two small supporting changes that did not change the planned behavior. I updated a stale repository comment that described updateEvent as future functionality and I updated the existing service method test to account for the newly exposed method. I did not add unrelated calendar features such as recurring events, notifications, or team assignment.

During the commit, the repository's pre commit hook ran the global formatter and modified many unrelated files because the repository already contains formatting differences. Only the nine intended files had been staged, so the implementation commit contained only those files. I discarded the unrelated formatter changes afterward and confirmed that the working tree was clean.

2026-11-01

I completed the final verification for the contribution and opened PR #134 against the CampusOS dev branch. The calendar test suite passed 115/115 tests, and I verified the implementation with the repository's lint, type check, build, and other required checks before opening the pull request.

2026-11-06

I worked on the changes requested by the maintainer. I added the calendar:updated event bus emission, optimized the service so full date updates do not require an unnecessary database read, added the VALIDATION_ERROR code, and documented the PATCH endpoint. I also added tests for the event bus behavior and the optimized date update case.

2026-11-09

I finished verifying the maintainer requested changes. The calendar suite passed 122/122 tests, lint, type check, and build completed successfully. I pushed the changes in commit c49419a and used the PR monitor to check the current PR state and generate a draft response. I rewrote the response, posted it after verifying that the commit was the PR head, and re-requested review from the maintainer. The Vercel deployment check remained failing, while my local calendar tests, lint, type check, and build passed.


**Toolkit**

- Tool: Claude Code, guided by my accepted implementation plan, followed by manual review and repository tests
- What it produced: The implementation added the calendar PATCH update path across the schema, service, controller, and routes, along with focused tests for the new behavior
- Difficulties: Partial date updates required validation against the stored event state and the pre commit formatter modified many unrelated files because of existing repository formatting differences
- What changed: I used the stored event to validate the final date range for partial updates, updated the existing service method test and stale repository comment, and discarded unrelated formatter changes after confirming that only the nine intended files were included in the commit

---

## Pull Request

**PR Link:** https://github.com/NITRR-Official/CampusOS/pull/134

**PR Description:** This PR adds PATCH /api/v1/calendar/:eventId for updating existing calendar events. It supports partial updates while preserving validation and the existing calendar:manage authorization. Partial date updates are validated against the stored event state to prevent invalid date ranges, and the existing repository updateEvent method is reused for persistence. The PR also adds focused tests for the new update behavior and fixes #23.

**Maintainer Feedback:**

- 2026-11-01: None yet, PR is awaiting maintainer review.

- 2026-11-05: The maintainer requested several changes before merge. The required change was to emit `calendar:updated` with the event ID and event type after a successful update. They also asked me to avoid an unnecessary database read for the full date updates, add a `VALIDATION_ERROR` code to the date-range error, and document the new PATCH endpoint.

- 2026-11-09: I addressed the requested changes in commit c49419a and added tests for the event bus emission and optimized date-update behavior. After verifying the changes with 122/122 calendar tests, lint, type check, and build, I responded to the maintainer and re-requested review.


**Status:** Awaiting review

**Toolkit**

- Tool: ship-gate, Claude Code, and PR monitor, used to verify the contribution, open the pull request, monitor its status, and respond to maintainer feedback
- What it produced: ship-gate verified the contribution before the PR was opened, Claude Code opened PR #134, and PR monitor identified the requested changes and later generated a draft response after the fixes were pushed
- Difficulties: The ship-gate hook did not trigger automatically through Claude Code, and PR monitor initially had Windows encoding and authentication issues
- What changed: I ran ship-gate manually, enabled Python UTF-8 mode for PR monitor, implemented and tested the maintainer's requested changes, rewrote the generated response in my own words, posted it through Claude Code, and re-requested review


---

## Learnings and Reflections

**Technical Skills Gained**

I learned how to add a PATCH endpoint within an existing backend architecture instead of building the update flow from scratch. I worked with partial request validation, service and repository interactions, RBAC permissions, and date-range validation that depends on both the request and stored event state. The maintainer feedback also taught me how the project's event bus is used for lifecycle events and how avoiding an unnecessary database read can make an update operation more efficient.


**Challenges Overcome**

One challenge was handling partial date updates because changing only `startsAt` or `endsAt` required validating the new value against the date already stored for the event. I handled this by retrieving the stored event only when the other date was needed for validation. Another challenge was keeping my contribution scoped when the repository's formatter modified hundreds of unrelated files, so I kept only my intended files staged and discarded the unrelated changes. I also worked through Windows encoding and authentication issues while using the PR monitor before I could successfully monitor and respond to the maintainer feedback.


**What I'd Do Differently Next Time**

Next time, I would review the repository's architecture decision record and related design documentation more closely before implementing the solution. This could have helped me identify the `calendar:updated` event bus requirement before opening the pull request. I would also establish the repository's testing and formatting baseline earlier so that preexisting failures are easier to separate from problems caused by my changes.

---

## Resources Used

- CampusOS issue #23: https://github.com/NITRR-Official/CampusOS/issues/23 - defined the calendar update endpoint requirements and was where I claimed the issue and communicated with the maintainer.

- CampusOS CONTRIBUTING.md: https://github.com/NITRR-Official/CampusOS/blob/dev/docs/contributing/CONTRIBUTING.md - helped me follow the repository's contribution process, required checks, and expected maintainer response times.

- CampusOS calendar reference documentation: https://github.com/NITRR-Official/CampusOS/blob/dev/docs/plugins/reference/calendar.md - helped me understand the existing calendar API and was updated during the maintainer requested changes to document the new PATCH endpoint.

- Maintainer review on PR #134: https://github.com/NITRR-Official/CampusOS/pull/134 - identified the missing `calendar:updated` event bus requirement, the redundant database read, error-code improvement, and documentation update that I addressed before re-requesting review.
