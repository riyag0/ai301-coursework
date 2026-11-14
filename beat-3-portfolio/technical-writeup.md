# Building a Calendar Event Update API for CampusOS



## Overview



I contributed to the CampusOS open source project by adding a calendar endpoint that allows users to update existing calendar events. Before my contribution, CampusOS could create and retrieve calendar events, but wasn't able to update the existing events in the calendar. To implement this, I added the PATCH endpoint along with validation and authorization.

After receiving the feedback from the maintainer, I made the requested code and documentation changes, tested them, and re-requested review.



PR link: https://github.com/NITRR-Official/CampusOS/pull/134



## What happened



I started by investigating the existing calendar code to understand what was missing and ran initial tests. I found that the repository already had an updateEvent method at the repository layer, but the API route/controller/service flow needed to be built. Before making any changes, I ran the existing calendar tests and 93/93 test cases passed. After establishing the baseline, I implemented the update path across the schema, service, controller, and routes, along with tests. After implementing the endpoint, I ran the tests again and the calendar suite increased from 93 to 115 passing tests, with all 6 test files passing. After opening the pull request, the maintainer reviewed my implementation and requested a few changes. The maintainer asked me to add the calendar:updated event, avoid an unnecessary database read, add the VALIDATION\_ERROR code, and document the PATCH endpoint. 



**Maintainer feedback:**



> "all calendar mutations must emit minimal lifecycle events so downstream modules (notifications, task sync, audit) can react"



> "update should emit calendar:updated with { eventId, eventType }"



Based on this feedback, I updated the implementation and added tests for the new behavior. After making these changes, I had 122/122 tests and other checks passing.



**Final test results:**



>  Test Files  6 passed (6)

>  Tests  122 passed (122)



After verifying the changes, I pushed the updated implementation, responded to the maintainer, and re-requested review.



## Limitations and what's next



One limitation is that the PR has not been merged yet and is awaiting another maintainer review. Next steps are to review any new feedback, make the requested changes, and test again before updating the PR.

