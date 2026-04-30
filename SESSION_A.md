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
   - start with a short plain-English section so a human can understand the
     intended change before the exact contract language
4. Hand off to Session B for spec-diff review.
5. Record decisions in response to review.
6. If the decisions change intended behavior, update `spec-diff.md`.
7. Write `plan.md`.
8. Hand off to Session B for plan review.
9. Record decisions in response to review.
10. If the decisions change intended behavior, update `spec-diff.md`.
11. If the decisions change implementation approach, update `plan.md`.
12. Implement.
13. Gather evidence.
14. Hand off to Session B for implementation review.
15. Record decisions and fix the issues that were accepted.
16. Repeat until accepted.
17. Update `SYSTEM.md`.
18. Update `CHANGELOG.md` and `commits.txt` if appropriate.

## Autonomous bucket mode

Autonomous bucket mode is the default once the human approves a roadmap
bucket as a stack of slices. Run the normal loop per slice without
stopping between slices unless an escalation gate trips. This keeps the
review surface small without making the human babysit every small
review.

Before entering this mode:

- propose the slice stack in plain English
- name the proof surface for each slice
- get human approval for the stack shape

While in this mode:

- create one phase folder per slice
- run Session B review automatically for spec/plan and implementation
- resolve non-controversial findings inside the active slice
- commit accepted slices before moving to the next one
- fold tiny review findings into the active slice instead of creating
  one-helper phases

Escalate to the human before continuing if:

- public API shape changes
- `SYSTEM.md` meaning would change beyond the approved spec diff
- reviewers disagree on the right semantic answer
- unsafe code, concurrency, memory ordering, or allocation claims change
- roadmap order or public positioning changes
- a finding requires product judgment rather than implementation judgment

Do not escalate for routine findings that are clearly implied by the
approved spec, such as missing tests, private refactors, proof-location
cleanup, or wording fixes. Resolve those inside the active slice and
record the decision.

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

## Talking to the human

The artifacts (`spec-diff.md`, `plan.md`, `reviews_and_decisions.md`)
are the durable record. The chat output is the human's only realistic
surface to act on it. Treat them as different audiences.

When you respond to findings or hand work back, your chat reply must:

- say in plain English what changed and why, not just "A3: accepted,
  N2: deferred"
- name the disagreements, the deferrals, and anything you decided
  alone that the human should know about
- ask explicitly for the decisions you cannot make alone
- link to the artifact as the receipt, not as the explanation

Do not write a chat reply that is mostly ID-only shorthand or "I
updated the plan, see the file." That sends the human into the file to
do work the chat surface should have done.

## Artifact split

- system meaning -> `spec-diff.md`
- implementation reasoning -> `plan.md`
- responses -> `reviews_and_decisions.md`
- proof -> tests, commands, logs, screenshots, or other evidence

## Guardrails

- do not skip the English step because the code looks easy
- do not let the plan become the place where intent gets decided
- do not silently resolve ambiguity in the plan
- do not update `SYSTEM.md` before proof
- do not treat the roadmap as the system baseline
- do not erase review history
