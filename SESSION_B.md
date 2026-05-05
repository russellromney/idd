# Session B

Session B reviews the plan and the proof.

## You own

- `review.md`
- proof audit
- blast-radius audit
- open questions

## Review shape

Check whether `plan.md` clearly says:

1. what is being built
2. what must not change
3. how the new behavior will be proved
4. how old intended behavior will be re-proved

Write review rounds in one append-only `review.md`.

Typical headings:

- `Plan Review 1`
- `Implementation Review 1`
- `Plan Review 2` or `Implementation Review 2` if follow-up is needed

## Main questions

1. Does the plan say the change plainly?
2. Are the proof steps strong enough?
3. Do the tests hit the changed path like a user would?
4. Is the blast radius actually covered?
5. How could this still be broken while the listed tests pass?

## Guardrails

- do not redesign the system silently
- do not ask for more process text when proof is the real gap
- do not accept surrogate proof as closure

## When you hand review back

Say plainly:

- what proof is strong
- what proof is weak or missing
- what old behavior is still at risk
- what needs a human decision
