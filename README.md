# idd

Intent-Driven Development, codified as a small working process.

This repo is a lightweight companion to my blog post
[Intent-Driven Development](https://russellromney.com/blog/intent-driven-development/).
It keeps the smallest useful artifact set first, while making two ideas
more explicit:

1. `reviews_and_decisions.md` is safer than a plain reviews.md` still living in one file.
2. Review should happen in a different session than planning and coding, and ideally by a different model family.

If you want to use this repo as a session bootstrap, start with
[START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md).

## What this is for

IDD exists for teams where code can be generated cheaply, but intent still needs an owner.

The process is meant to protect against intent drift:

- code that works but changes the system into something you did not mean to build
- plans that quietly redefine the intended change
- reviews that get overwritten by responses
- specs that become fiction after the code moves

This repo is deliberately small. If the text files do not hurt yet, do
not add more tooling.

## Core ideas

- `SYSTEM.md` is the current English model of the system.
- Every meaningful change starts with a spec diff.
- The plan is implementation reasoning, not new intent.
- Review happens against the spec diff, not against vibes.
- Decisions respond to review findings and say what changes because of
  them.
- `SYSTEM.md` only updates after the implementation proves it deserves
  to become the new baseline.

## Artifact set

For a small project, the default artifact set is:

```text
.intent/
  SYSTEM.md
  phases/
    001-phase-name/
      spec-diff.md
      plan.md
      reviews_and_decisions.md
      commits.txt
```

This repo also includes templates for those files in
[`/.intent/templates/`](</Users/russellromney/Documents/Github/idd/.intent/templates>).
It also includes one worked example phase in
[`/.intent/phases/000-example-lease-contract/`](</Users/russellromney/Documents/Github/idd/.intent/phases/000-example-lease-contract>).

For fast orientation in a new session, also see:

- [START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md)
- [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
- [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)

## Recommended loop

The simplest useful loop uses two sessions:

1. Session A owns baseline checks, the spec diff, and the plan.
2. Session B reviews the plan against the spec diff.
   Prefer a different model family from Session A when possible.
3. Session A records decisions in response to the review.
   If those decisions change intent, update the spec diff.
   If they change implementation approach, update the plan.
4. Session A implements and gathers evidence.
5. Session B reviews the implementation against the spec diff.
6. Session A records decisions and fixes in response.
7. Repeat steps 5-6 until the phase is accepted.
8. Only then update `SYSTEM.md` and record the resulting commits.

This separation is intentional:

- Session A should preserve continuity of intent and implementation.
- Session B should be freer to criticize that work.
- Different session context makes it harder for the reviewer to simply
  ratify the earlier reasoning.
- A different model family is even better when available.

## Reviews and decisions

The review file should stay append-only.

- Review rounds record critique.
- Decision rounds record responses.
- Review findings get stable IDs like `P1`, `N2`, `A1`.
- Decisions reference those IDs directly.
- Do not rewrite earlier review text to make it look resolved.

That gives you a clean trail:

- what the reviewer thought
- what the implementer accepted or rejected
- what changed because of that judgment

## Artifact roles

- `SYSTEM.md`
  current baseline only; not a wishlist
- `spec-diff.md`
  normative intent for this phase
- `plan.md`
  implementation reasoning and verification approach
- `reviews_and_decisions.md`
  critique plus explicit responses, by round
- `commits.txt`
  evidence trail linking the phase to actual commits

Keep those names stable.

- use `reviews_and_decisions.md`, not a mix of `review.md`,
  `reviews.md`, and other nearby names
- keep one phase folder per meaningful change
- let history live in round sections inside the file before inventing
  more structure
## Where thinking should go

Use this rule:

- if it changes what the system is supposed to do, it belongs in the  spec diff
- if it explains how to build or verify the change, it belongs in the  plan
- if it argues about whether an interpretation is acceptable, it belongs in reviews and decisions

If planning uncovers ambiguity, do not silently resolve intent in the
plan. Flag it there and let review and decision rounds adjudicate it.

## What Is Working In Practice

Looking at live repos already using this workflow, a few patterns seem
worth codifying:

- The strongest plans do more than list steps.
  They map the spec diff to implementation, state phase decisions
  explicitly, define the build order, and call out risks.
- `Context`, `References`, `Traps`, `Acceptance`, and `Commands` are
  useful optional plan sections when the phase is non-trivial.
  They should be used when they reduce ambiguity, not by default in
  every tiny phase.
- Reviews get much better when they name the artifacts reviewed and the
  evidence reviewed.
- Responses to review findings should not overwrite the review itself.
  That is why `reviews_and_decisions.md` exists.
- `commits.txt` is still useful before commits exist.
  It can temporarily record "no commit yet" plus the current local work
  and verification evidence.

So the standard here is:

- keep the artifact set small
- standardize names hard
- use richer sections only when the phase complexity justifies them

## Keep it small

This repo is intentionally conservative about structure.

If you only need one review round, one `reviews_and_decisions.md` file
is enough. If phases start needing multiple review rounds regularly,
append them in the same file before inventing more directories.

The test for a new artifact is simple:

- does it reduce ambiguity enough to justify being maintained?

If not, it is probably making IDD worse instead of better.

## Notes on roadmap and changelog

The author sometimes uses a roadmap/changelog structure, especially in more vibey projects. The roadmap is both for basic ideas and structured plans, while the changelog is for the completed plans. 

The author is currently moving away from the roadmap/changelog process because they created a lot of ambiguity about what is vs what will be. Agents constantly conflated the two and the files got really long.

`ROADMAP.md` and `CHANGELOG.md` are useful companion artifacts, but they play different roles from the core IDD files.

- `ROADMAP.md` is upstream of a phase. It is for future direction, prioritization, and possible work.  It is intentionally aspirational and non-normative. A roadmap item can motivate a spec diff, but it should not replace  one.
- `CHANGELOG.md` is downstream of a phase. It is for summarizing what actually landed. It is historical and communicative, not the source of current system truth.

That means:

- do not review implementation against the roadmap
- do not treat the changelog as the current system model
- do treat the roadmap as the place ideas wait before becoming a spec diff
- do treat the changelog as the place accepted phases get summarized after they land

The usual flow is:

* `ROADMAP.md` 
* -> `spec-diff.md` 
* -> `plan.md` 
* -> `reviews_and_decisions.md`
* -> implementation and evidence 
* -> `SYSTEM.md` 
* update -> `CHANGELOG.md`

If a phase changes the intended future direction, update the roadmap. If a phase changes the current proved baseline, update `SYSTEM.md`. If a phase lands, summarize it in the changelog.
