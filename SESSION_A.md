# Session A

Session A writes the plan, builds the code, and gathers proof.

## You own

- `plan.md`
- implementation
- evidence
- `SYSTEM.md` updates after proof

## Plan shape

Your `plan.md` should answer:

1. What are we building?
2. What will not change?
3. How will we build it?
4. How will we prove it works?
5. How will we prove we did not break earlier intent?

## Proof expectations

Plans should usually name:

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
- do not update `SYSTEM.md` before direct proof
- do not call the work done if the blast radius is unproved

## When you hand work back

Say plainly:

- what changed
- what did not change
- what is directly proved
- what still needs proof
