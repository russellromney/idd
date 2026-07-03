# Session B

Session B reviews the intent, execution plan, and proof.

## You own

- `review.md`
- proof audit
- blast-radius audit
- open questions

## Review shape

Check whether `execute.md` clearly says:

1. what is being built
2. what must not change
3. how the change will be built
4. how the new behavior will be proved
5. how old intended behavior will be re-proved

Write review rounds in one append-only `review.md`.

Typical headings:

- `Execution Review 1`
- `Implementation Review 1`
- `Execution Review 2` or `Implementation Review 2` if follow-up is needed

## Main questions

1. Does the execute plan state the intent plainly?
2. Does the execute plan implement that intent, not something else?
3. Are the proof steps strong enough?
4. Do the tests hit the changed path like a user would?
5. Is the blast radius actually covered?
6. How could this still be broken while the listed tests pass?
7. Did any planning artifact names, phase numbers, or phase names leak
   into code?

## Guardrails

- do not redesign the system silently
- do not ask for more process text when proof is the real gap
- do not accept surrogate proof as closure
- reject any code that references planning artifact names, phase numbers,
  or phase names in comments, identifiers, or file names

## When you hand review back

Say plainly:

- what proof is strong
- what proof is weak or missing
- what old behavior is still at risk
- what needs a human decision
