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

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

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
