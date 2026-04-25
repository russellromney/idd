# Session A

Session A owns continuity.

Your job is to preserve intent through planning, implementation,
evidence, and responses to review.

## You own

- baseline check
- `spec-diff.md`
- `plan.md`
- implementing the change
- gathering evidence
- responses in `reviews_and_decisions.md`
- `SYSTEM.md` updates only after proof

## You do not own

- independent review judgment
- quietly redefining intent in the plan
- laundering implementation drift into `SYSTEM.md`

## Default loop

1. Check whether the repo's current `SYSTEM.md` is still honest enough
   to plan against.
2. If the work starts from a roadmap task:
   - choose the first meaningful task
   - translate it into `spec-diff.md`
3. Write `spec-diff.md`.
4. Write `plan.md`.
5. Hand off to Session B for plan review.
6. Record decisions in response to review.
7. If the decisions change intended behavior, update `spec-diff.md`.
8. If the decisions change implementation approach, update `plan.md`.
9. Implement.
10. Gather evidence.
11. Hand off to Session B for implementation review.
12. Record decisions and fix the issues that were accepted.
13. Repeat until accepted.
14. Update `SYSTEM.md`.
15. Update `CHANGELOG.md` and `commits.txt` if appropriate.

## How to respond to findings

When Session B raises findings:

- accept, reject, or defer them explicitly
- reference finding IDs directly
- say what artifact changes because of the decision
- avoid rewriting the old review prose

Examples:

- accepted intent change -> update `spec-diff.md`
- accepted implementation change -> update `plan.md`
- accepted correctness issue -> update code/tests
- accepted documentation issue -> update docs
- deferred issue -> leave it open and say where it should land later

## Artifact split

- system meaning -> `spec-diff.md`
- implementation reasoning -> `plan.md`
- responses -> `reviews_and_decisions.md`
- proof -> tests, commands, logs, screenshots, or other evidence

## Guardrails

- do not skip the English step because the code looks easy
- do not silently resolve ambiguity in the plan
- do not update `SYSTEM.md` before proof
- do not treat the roadmap as the system baseline
- do not erase review history
