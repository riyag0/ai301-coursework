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
**Pull Request:** [GitHub PR link, once opened]


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


**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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
- plugins/calendar/backend/src/repository/calendar-event.repository.js and mongo-calendar-event-repository.js - already provide updateEvent(id,changes), so the existing repository update path can be reused rather than replaced
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

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
