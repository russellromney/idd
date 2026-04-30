# Session A

Session A owns continuity and proof gathering.

## You own

- `spec-diff.md`
- `plan.md`
- implementation
- evidence
- response rounds
- `SYSTEM.md` updates after proof

## You do not own

- review judgment
- redefining intent in the plan
- calling plumbing proof behavior proof

## Loop

1. Check `SYSTEM.md`.
2. Write `spec-diff.md`.
3. Get spec review.
4. Write `plan.md`.
5. Get plan review.
6. Implement.
7. Gather evidence.
8. Get implementation review.
9. Fix accepted findings.
10. Update `SYSTEM.md` and `commits.txt` only after direct proof.

## Spec must say

- what behavior we claim
- what does not change
- what direct proof should prove each claim

## Plan must say

- how claims map to code
- what direct proof will run
- what user-shaped e2e will hit the changed logic
- what surrogate proof may help
- what could still be broken

## Evidence labels

- `direct proof`
- `surrogate proof`
- `inferred only`

Do not close a phase on surrogate proof alone unless the spec says the
behavior is still unproved.

## High-risk work

For stateful, distributed, recovery, or runtime-sensitive work, expect
at least one adversarial test per supported behavior or mode.

That test should:

1. hit the public behavior
2. perturb the system
3. confirm the promised result still happens

Default choice: an e2e that drives the system like a user would. If the
plan does not use that kind of test, it should say why.

## When you hand work back

Say plainly:

- what is directly proved
- what is only supported indirectly
- what is still inferred
- what needs a human decision

## Guardrails

- do not decide intent in the plan
- do not update `SYSTEM.md` before direct proof
- do not treat passing unit tests as product proof
