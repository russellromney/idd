# Session A

Session A writes the intent and execution plan, builds the code, and gathers proof.

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

Execution plans should usually name:

- unit proof
- integration proof
- e2e proof
- blast-radius proof

Default proof for changed behavior:

- an e2e or integration flow that uses the public path and hits the
  changed logic

If you do not have that kind of proof, say why.

## Guardrails

- do not hide intent in implementation prose
- do not treat helper tests as enough by themselves
- do not use `execute.md` for discovery, auditing, or redefining intent
- do not put planning artifact names, phase numbers, or phase names in
  code comments, identifiers, or file names
- do not call the work done if the blast radius is unproved

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
