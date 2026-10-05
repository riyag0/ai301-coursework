# Voice guide: how I talk upstream

<!--
THIS IS A CARRY-OVER SLOT, not a new hole. You wrote this guide in
week 2; paste your filled week-2 voice-guide.md here, whole. It is not
re-authored and it is not graded as new work this week.

Then reread it with the plan comment in mind. Your claim and repro
comments promised and reported; a plan comment commits you to an
approach in front of the people who maintain the code. If your rules
do not cover that register (for example: how you state an approach you
are not certain of, or how you respond when a maintainer already
suggested a direction), extend the guide with what it needs. Extending
is allowed and encouraged; starting over is not required.

Live mode reads this file before your plan comment goes out and
reports any rule your draft breaks. Eval mode ignores it entirely,
because your voice is yours and carries no gold labels.
-->

## Who I am in threads

<!-- Paste your week-2 section here. -->
I am a recent CS graduate making my first open source contribution as part of a structured course project. I am new to this specific contribution process, though not new to writing and testing code.

## Rules I write by

<!-- Paste your week-2 rules here, wrong/right pairs and all. Add any
rule the plan-comment register needs that your week-2 comments did
not. -->
## Rule : Promise investigation, not outcomes

I say what I am going to look into not what I will deliver or when. I don't commit to a fix, a timeline, or a result I haven't verified yet.

Wrong: I will have a fix for this by tomorrow.
Right: I am going to look into this and report back what I find.

## Rule: State only what I actually observed

I don't claim a reproduction succeeded unless my own evidence shows the exact behavior the issue describes. 

Wrong: Yup, this happens, can confirm
Right: I ran the steps in the issue on version X and did not see the described behavior, here is what I saw instead.

## Rule: Be specific, not generic

Every comment names the actual file, command, or output involved.

Wrong: Looking into this now, will update soon.
Right: I am setting up the dev environment with docs/SETUP.md and will reproduce using the steps in the issue body.

## Rule: Disclose AI assistance when the repo requires it

If a repo's contribution policy requires disclosing AI tool use, I state it rather than leaving it out.

Wrong: Saying nothing about AI assistance when the repo's contribution policy requires it.
Right: I used Claude to help draft this report, I reviewed and verified the reproduction steps myself.

## Rule: Commit to a plan, not a delivery date

My plan comment states what I intend to build and why, not when it will be done or merged. I don't promise a PR timeline, even an approximate one.

Wrong: Will send the PR shortly
Right: Plan is one change fix in the sync controller's push callback. Next step is building and testing it.


## Things I never post

<!-- Paste your week-2 list here; extend it if planning tempts you
toward new ones (overpromised timelines are the classic). -->
- I never promise a fix, a pull request, or a timeline before I have actually reproduced the issue.
- I never claim a reproduction succeeded based on assumption or pattern matching to similar issues.
- I never leave out required AI disclosure language when a repo's policy asks for it.
- I never promise a PR timeline in a plan comment
