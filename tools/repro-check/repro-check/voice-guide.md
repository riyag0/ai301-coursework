# Voice guide: how I talk upstream

<!--
THIS IS THE PART YOU WRITE (new this week). Live mode reads this file
before any comment of yours goes out the door; eval mode ignores it
entirely, because your voice is yours and carries no gold labels.

This is not etiquette. "Be polite and concise" is advice for everyone
and therefore rules for no one. Write rules YOU need, in your own
words, each one concrete enough that the skill can hold a draft
against it and say which rule it breaks.

Three sections. Fill all three.
-->

## Who I am in threads

<!-- 2-3 lines. Who is talking when you comment on an issue: your
experience level stated plainly, what you are doing in this repo, what
readers can expect from you. This is the register your rules protect. -->

I am a recent CS graduate making my first open source contribution as part of a structured course project. I am new to this specific contribution process, though not new to writing and testing code.

## Rules I write by

<!-- 3-5 rules, drafted from the lecture's slide-12 moment. Each rule
needs a wrong/right pair from your own hand: one line you might
actually have written that breaks the rule, and the line you would
post instead. The pair is what makes a rule executable; a rule without
one is a wish.

Format each rule like this:

### Rule: <short name>

<The rule, one or two sentences.>

- Wrong: "<a line that breaks it>"
- Right: "<the line to post instead>"
-->
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


## Things I never post

<!-- A short list. Promises you cannot keep, tones you refuse,
shortcuts you know you reach for when tired. The skill quotes this
list back at you when a draft crosses it. -->

- I never promise a fix, a pull request, or a timeline before I have actually reproduced the issue.
- I never claim a reproduction succeeded based on assumption or pattern matching to similar issues.
- I never leave out required AI disclosure language when a repo's policy asks for it.