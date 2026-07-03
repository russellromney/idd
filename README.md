# idd

Intent-Driven Development.

Goal: say what we are building, say what must not change, and prove
both.

Start with [START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md).

## Core questions

Every phase answers:

1. What are we building?
2. What will not change?
3. How will we prove it works?
4. How will we prove we did not break earlier intent?

If these are unclear, the phase is not ready.

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

- `execute.md`: what and how we build, and how we prove it
- `review.md`: append-only reviews
- `commits.txt`: what landed with what proof

## Rules

1. Do not implement from `ROADMAP.md`.
2. `execute.md` is for intent and implementation. not discovery or
   auditing.
3. Every changed behavior needs direct proof.
4. Every risky change needs blast-radius proof.
5. Prefer user-shaped e2e for changed behavior.
6. Surrogate proof is not enough.
7. Never put planning artifact names, phase numbers, or phase names in
   code.

## Proof terms

`direct proof`
- proves the claimed behavior

`surrogate proof`
- proves something nearby

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

For high-risk work, include one e2e or integration flow that hits the
public path, exercises the changed logic, and confirms the promised
result.

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
