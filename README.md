# idd

Intent-Driven Development, pared down to the smallest process that still
protects intent and proves behavior.

This repo is a lightweight companion to the blog post
[Intent-Driven Development](https://russellromney.com/blog/intent-driven-development/).

If you want to bootstrap a new session, start with
[START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md).

## The problem this process is trying to solve

Code can compile, unit tests can pass, reviews can look careful, and the
actual thing we meant to build can still be broken.

That usually happens because we prove nearby facts instead of the
behavior we actually care about.

Examples:

- bootstrap works, but the first real write does not
- a manifest exists, but the follower never sees the leader's data
- role wiring is consistent, but failover never completes
- the tests prove plumbing, not the product behavior

IDD exists to stop that.

## Five rules

1. `SYSTEM.md` is current truth, not aspiration.
2. Every phase starts with a `spec-diff.md`.
3. Every behavior claim needs a direct executable proof.
4. Surrogate proof can support a claim, but cannot close it.
5. `SYSTEM.md` only updates after direct proof.

If a claim does not have a direct proof, the phase can still ship code,
but it cannot honestly claim that behavior is proved.

## Default artifact set

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

Also included:

- templates in
  [`/.intent/templates/`](</Users/russellromney/Documents/Github/idd/.intent/templates>)
- a worked example in
  [`/.intent/phases/000-example-lease-contract/`](</Users/russellromney/Documents/Github/idd/.intent/phases/000-example-lease-contract>)
- session bootstrap docs:
  - [START_HERE.md](/Users/russellromney/Documents/Github/idd/START_HERE.md)
  - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
  - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)

## Artifact roles

- `SYSTEM.md`
  proved baseline of the system today
- `spec-diff.md`
  intended behavior change for one phase
- `plan.md`
  implementation approach and proof plan
- `reviews_and_decisions.md`
  append-only critique and responses
- `commits.txt`
  what actually landed and what evidence existed

The files matter, but they are not the process. The process is:

- state the intended behavior
- name the direct proof
- build the code
- try to falsify the claim
- only then call it done

## Direct proof versus surrogate proof

Use these words explicitly.

**Direct proof**

- directly demonstrates the behavior claimed in the spec
- examples:
  - leader writes, follower reads the row
  - leader dies, follower promotes, writes still succeed
  - HTTP client follows redirect and request succeeds

**Surrogate proof**

- proves supporting facts nearby, but not the behavior itself
- examples:
  - manifest exists
  - bootstrap completed
  - helper function unit tests pass
  - mode validation rejects bad inputs

**Missing proof**

- no executable check directly covers the claim yet

Surrogate proof is useful. It is just not enough by itself.

## The question every review must ask

For every claimed behavior:

> How could this still be completely broken while the current tests all pass?

If the answer is easy, the proof is not strong enough yet.

That question is especially important for HA, replication, failover,
coordination, and startup sequencing work.

## Session split

Session A owns:

- baseline check
- `spec-diff.md`
- `plan.md`
- implementation
- evidence gathering
- responses to review

Session B owns:

- skepticism
- proof-audit review
- implementation review
- follow-up review rounds

Prefer a different model family for Session B when possible.

## Minimal loop

1. Session A writes `spec-diff.md`.
   It must name the behavior claims and the direct proof expected for
   each claim.
2. Session B reviews the spec.
   Most importantly: are the claims clear, and is the proposed proof
   actually direct?
3. Session A writes `plan.md`.
   The proof plan comes before implementation details.
4. Session B reviews the plan.
   Most importantly: does the plan actually produce the required proof?
5. Session A implements and gathers evidence.
6. Session B reviews the implementation and the evidence.
   Most importantly: did the code prove the claimed behavior, or only a
   surrogate?
7. Session A fixes accepted findings.
8. Only then update `SYSTEM.md`, `commits.txt`, and optionally
   `CHANGELOG.md`.

## What a good phase looks like

A good phase folder answers four simple questions:

1. What behavior are we claiming?
2. What does not change?
3. What exact command or test directly proves the claim?
4. What is still only inferred?

If the folder cannot answer those questions quickly, it is probably too
clever or too vague.

## Keep it small

Do not add more artifacts to compensate for weak proof.

If verification is weak, fix verification.
If the claim is fuzzy, fix the spec.
If the plan is making semantic decisions, push them back into the spec
or a decision round.

The point is not to produce more process text. The point is to make it
hard to lie to ourselves about whether the code does the thing we meant.
