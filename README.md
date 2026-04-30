# idd

Intent-Driven Development, codified as a small working process.

This repo is a lightweight companion to the blog post
[Intent-Driven Development](https://russellromney.com/blog/intent-driven-development/).

If you want to use this repo to bootstrap a new session, start with
[START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md).

## What this is for

IDD exists for teams where code is cheap but intent still needs an
owner.

The process is meant to reduce:

- code that works but changes the system you meant to build
- plans that quietly redefine intent
- reviews that get overwritten by responses
- specs that stop matching the code

This repo is intentionally small. If the text files do not hurt yet, do
not add more tooling.

## Why this exists

This process exists because a few failure modes show up over and over:

- code can be correct in isolation while still changing the intended
  system
- plans can quietly become the place where intent gets rewritten
- reviews can get overwritten by responses until the critique disappears
- roadmap-style docs often blur what already is true with what might be
  true later

IDD is an attempt to keep those concerns separate without adding heavy
  process.

## Default artifact set

```text
.intent/
  SYSTEM.md
  phases/
    0001-phase-name/
      spec-diff.md
      plan.md
      reviews_and_decisions.md
      commits.txt
```

Also included:

- templates in
  [`/.intent/templates/`](</Users/russellromney/Documents/Github/idd/.intent/templates>)
- a worked example in
  [`/.intent/phases/000-example-lease-contract/`](</Users/russellromney/Documents/Github/idd/.intent/phases/000-example-lease-contract>)
- session bootstrap docs:
  - [START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md)
  - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
  - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)

## Core rules

- `SYSTEM.md` is current baseline, not aspiration
- every meaningful change starts with a `spec-diff.md`
- `spec-diff.md` should start with a short plain-English section for humans
- the plan should not have to make intent decisions for us
- `plan.md` is implementation reasoning, not new intent
- review against the spec diff, not just the plan
- use `reviews_and_decisions.md`, not ad hoc review filenames
- keep review text append-only
- update `SYSTEM.md` only after proof

## Session split

Session A owns:

- baseline checks
- `spec-diff.md`
- `plan.md`
- implementation
- evidence gathering
- responses to review findings

Session B owns:

- spec-diff review
- plan review
- implementation review
- follow-up review rounds

Prefer a different model family for Session B when possible.

That separation is not just stylistic. It makes it harder for the
review step to merely ratify the reasoning that already happened in
Session A.

## Recommended loop

1. Session A writes `spec-diff.md`.
2. Session B reviews the spec diff.
3. Session A records decisions and updates the spec diff if needed.
4. Session A writes `plan.md`.
5. Session B reviews the plan against the spec diff.
6. Session A records decisions and updates the plan or spec diff if
   needed.
7. Session A implements and gathers evidence.
8. Session B reviews the implementation against the spec diff.
9. Session A records decisions and fixes accepted findings.
10. Repeat until accepted.
11. Only then update `SYSTEM.md`, `commits.txt`, and optionally
   `CHANGELOG.md`.

## Autonomous bucket mode

Autonomous bucket mode is the default for approved roadmap work that
can be split into reviewable slices. This is similar to stacked diffs:
the human approves the shape of the stack, then agents run each slice
through the normal spec-plan-implementation-review loop independently.

Use this mode when:

- the roadmap bucket is directionally clear
- the work can be split into ordered semantic slices
- each slice has a concrete proof surface
- the main cost is human round-tripping, not unresolved intent

The default autonomous loop is:

1. Session A proposes the slice stack for the bucket.
2. The human approves the stack or adjusts it.
3. For each slice, Session A writes `spec-diff.md` and `plan.md`.
4. Session B reviews automatically.
5. Session A resolves non-controversial findings automatically.
6. Session A implements, gathers evidence, and requests implementation
   review automatically.
7. Session A fixes accepted findings, records decisions, and commits the
   accepted slice.
8. Session A continues to the next slice until an escalation gate trips or
   the bucket is complete.

Escalate to the human instead of continuing autonomously when:

- public API shape changes
- `SYSTEM.md` meaning would change beyond the approved spec diff
- reviewers disagree on the right semantic answer
- unsafe code, concurrency, memory ordering, or allocation claims change
- roadmap order or public positioning changes
- a finding requires product judgment rather than implementation judgment

Examples:

- escalate when adding or changing a public trait, protocol, schema, or
  compatibility promise
- escalate when two plausible semantic interpretations fit the spec
- escalate when the review says the chosen design is wrong, not merely
  under-tested
- do not escalate for a missing test that proves already-agreed behavior
- do not escalate for private refactors that preserve the spec and proof
- do not escalate for wording fixes in `plan.md` or
  `reviews_and_decisions.md`

Tiny findings should stay inside the active slice. Add the missing test,
clarify the sentence, or move the proof location without creating a new
phase unless the behavior or system intent changes.

## Artifact roles

- `SYSTEM.md`
  current proved system model
- `spec-diff.md`
  intended semantic change for one phase
- `plan.md`
  implementation reasoning
- `reviews_and_decisions.md`
  critique plus explicit responses, by round
- `commits.txt`
  evidence trail tied to actual commits

Stable names matter. Prefer one phase folder per meaningful change and
one `reviews_and_decisions.md` file with append-only rounds.

## Where thinking should go

- system meaning -> `spec-diff.md`
- implementation reasoning -> `plan.md`
- argument about acceptable interpretation -> `reviews_and_decisions.md`

If planning uncovers ambiguity, flag it there. Do not silently resolve
intent inside the plan. The plan should not have to make intent
decisions for us.

## Roadmap and changelog

`ROADMAP.md` and `CHANGELOG.md` are optional companion artifacts.

They can still be useful, especially in more vibey projects, but they
also create a recurring ambiguity: what is true now versus what might be
true later. In practice, agents often conflate those two unless the repo
is very explicit.

- `ROADMAP.md` is upstream of a phase.
  It is for future direction, prioritization, and candidate work.
- `CHANGELOG.md` is downstream of a phase.
  It summarizes what actually landed.

So:

- do not review against the roadmap
- do not treat the changelog as current system truth
- do treat the roadmap as the place ideas wait before becoming a spec
  diff
- do treat the changelog as the place accepted phases get summarized

Typical flow:

`ROADMAP.md` -> `spec-diff.md` -> `plan.md` ->
`reviews_and_decisions.md` -> implementation and evidence -> `SYSTEM.md`
-> `CHANGELOG.md`

## What is working in practice

From live repos already using this process:

- plans work best when they map the spec diff to implementation and call
  out phase decisions, build order, and risks
- spec diffs work better when they open with a short plain-English summary
  before the exact contract language
- optional sections like `Context`, `References`, `Traps`,
  `Acceptance`, and `Commands` help on non-trivial phases
- reviews get better when they name the artifacts and evidence reviewed
- response text should not overwrite review text
- `commits.txt` is still useful even before commits exist

Those patterns were not invented in the abstract here; they showed up
while using the workflow in real repos like `bouncer`, `knocker`, and
`tina-rs`.

## Keep it small

- use richer sections only when the phase complexity justifies them
- one `reviews_and_decisions.md` file is enough until it hurts
- add new artifacts only if they reduce ambiguity enough to justify
  maintenance
