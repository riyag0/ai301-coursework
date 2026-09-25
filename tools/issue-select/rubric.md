# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer is active | last 5 default branch commits under Repo facts | At least one of the last 5 default branch commits is dated within 90 days of the capture date (eval) / today (live) | required |
| Repo in use | archived: flag and last push to any branch under Repo facts (live: archived banner, front page newest commit date)| Repo is not archived and the last push is within 180 days of the capture date (eval) / today (live) | required |
| Scope fits a newcomer | Issue body, comment thread, and linked PRs under repo facts | Fails only if issue is an umbrella/tracking issue whose sub items are meant to be split into separate issues, not a single cohesive feature or doc topic broken into checklist or the thread shows an unresolved design debate with no maintainer decision, including cases where contributors are reverse engineering undocumented external behavior with no settled spec or maintainer states the fix touches core internals or it is a pure usage/support question or the issue depends on a specific undecided input the assignee cannot supply themselves, such as an unspecified asset (e.g. a logo, image, or file marked TBD) or an undecided cross package boundary, or the issue has two or more closed/abandoned linked PRs, or the thread shows two or more separate contributors each claiming the issue and then going stale/unresponsive, signaling real difficulty despite apparent simplicity. A short list of concrete named examples (even ending in etc.) is a bounded starting point, not an unresolved scope. A checklist, multiple related sub tasks on one topic, or reporter's own suggested implementation approaches do not by themselves fail this check | required |
| Nobody else is already on it | this issue: assignees: , linked PRs: and comments section under repo facts |  No assignee listed, no open linked PR, and no unanswered "I will take this" comment posted within the last 30 days | required |
| AI assisted contributions allowed | contribution policy line under repo facts | Fails only if the policy contains an outright ban on AI generated code | required |


## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." --> Accept if every required check passes. A single required check fail or unclear rejects the issue. Unclear is treated as fail for all checks (no exceptions). Preferred checks never affects the verdict; they only rank accepted issues, with more preferred check passes ranking higher.