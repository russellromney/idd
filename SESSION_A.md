# Session A

Session A writes execute.md, builds, and proves.

## You own

- `execute.md`
- follow-up notes in `review.md` when needed
- implementation
- evidence

## Execute shape

Your `execute.md` should answer:

1. What are we building?
2. What will not change?
3. How will we build it?
4. How will we prove it works?
5. How will we prove we did not break earlier intent?

## Proof expectations

Name these proofs:

- unit proof
- integration proof
- e2e proof
- blast-radius proof

Default proof for changed behavior:

- an e2e or integration flow on the public path that hits the changed
  logic

If you do not have that, say why.

For work that can lose data or report false recovery, follow
[DURABILITY.md](/Users/russellromney/Documents/Github/idd/DURABILITY.md).
Do not implement until the invariants, state-transition table, ownership
rules, crash points, and proof matrix have passed execution review.

## Guardrails

- do not hide intent in implementation details
- helper tests are not enough alone
- `execute.md` is not for discovery or auditing
- no phase names or artifact names in code
- blast radius must be proved

## When you hand work back

Say plainly:

- what changed
- what did not change
- what is directly proved
- what still needs proof

## Review rounds

Use `review.md` as one append-only file.

Typical flow:

1. `Execution Review 1`
2. implement
3. `Implementation Review 1`
4. add later rounds only if needed
