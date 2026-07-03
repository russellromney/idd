# idd

Intent-Driven Development.

Goal: say what we are building, say what must not change, and prove
both.

Start with [START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md).

## Core questions

Every phase should answer, in plain English:

1. What are we building?
2. What will not change?
3. How will we prove it works?
4. How will we prove we did not break earlier intent?

If a phase cannot answer those clearly, it is not ready.

## Default files

```text
.intent/
  phases/
    0001-phase-name/
      execute.md
      review.md
      commits.txt
```

## File roles

- `execute.md`: what we are building, how we will build it, and how we
  will prove it
- `review.md`: append-only execution and implementation review rounds
- `commits.txt`: what landed and what proof existed

## Rules

1. Do not implement from `ROADMAP.md`.
2. `execute.md` states intent and implementation, not discovery or
   auditing.
3. Every changed behavior needs direct proof.
4. Every risky change needs blast-radius proof.
5. Prefer e2e that hits the changed path like a user would.
6. Surrogate proof helps, but does not close the claim.
7. Planning artifact names, phase numbers, and phase names must never
   appear in code comments, identifiers, file names, or other
   implementation details.

## Proof terms

`direct proof`
- proves the claimed behavior

`surrogate proof`
- proves a nearby fact

`blast-radius proof`
- proves old intended behavior still holds

`missing proof`
- no executable proof yet

## Main idea

The process is not:

- write artifacts
- get review
- pass a gate

The process is:

1. state the change
2. state the non-change
3. build it
4. assault the invariant with tests
5. keep going until the proof is real

## Default proof shape

A good execute.md usually includes:

- unit tests for local logic
- integration tests for joins between pieces
- e2e tests for user-visible behavior
- adversarial tests for risky paths

For high-risk work, the default proof should include at least one e2e
or integration flow that:

1. hits the public path
2. exercises the changed logic
3. perturbs the system if needed
4. confirms the promised result still happens

## Review question

For every claim, ask:

> How could this still be broken while the current tests pass?

If the answer is easy, the proof is weak.

## Review shape

Use one `review.md` file per phase.

Keep it append-only.

It should usually contain:

- `Execution Review 1`
- `Implementation Review 1`
- later follow-up rounds only if needed
