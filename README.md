# idd

Intent-Driven Development.

Goal: keep intent clear and prove behavior.

Start with [START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md).

## Problem

Code can look good and still not do the thing we wanted.

That usually happens because we prove nearby facts, not the behavior
itself.

## Five rules

1. `SYSTEM.md` is current truth.
2. Every phase starts with `spec-diff.md`.
3. Every behavior claim needs direct proof.
4. Surrogate proof helps, but does not close the claim.
5. Update `SYSTEM.md` only after direct proof.

## Default files

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

## File roles

- `SYSTEM.md`: current baseline
- `spec-diff.md`: intended behavior change
- `plan.md`: build plan and proof plan
- `reviews_and_decisions.md`: append-only critique and responses
- `commits.txt`: what landed and what proof existed

## Process

1. State the behavior.
2. Name the direct proof.
3. Build the code.
4. Try to falsify the claim.
5. Call it done only if the proof holds.

## Proof terms

`direct proof`
- proves the claimed behavior

`surrogate proof`
- proves a nearby fact

`missing proof`
- no executable check proves the claim yet

## Review question

For every claim, ask:

> How could this still be broken while the current tests pass?

If the answer is easy, the proof is weak.

## Minimal loop

1. Session A writes `spec-diff.md`.
2. Session B reviews the spec.
3. Session A writes `plan.md`.
4. Session B reviews the plan.
5. Session A implements and gathers evidence.
6. Session B reviews code and proof.
7. Session A fixes accepted findings.
8. Then update `SYSTEM.md` and `commits.txt`.

## A good phase answers four questions

1. What behavior are we claiming?
2. What does not change?
3. What exact test or command proves the claim?
4. What is still inferred?

## Keep it small

If proof is weak, fix proof.

Do not add more artifacts to hide weak verification.
