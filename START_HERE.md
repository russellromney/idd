# Start Here

Use this when a session is told:

> look at `../idd` and init here

## Order

1. Read this file.
2. Decide if you are Session A or Session B.
   - default: Session A
   - review/audit: Session B
3. Read the matching card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)
4. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md)
   only if you need more context.

## Hard rules

- do not implement from `ROADMAP.md`
- review against `spec-diff.md`
- keep `reviews_and_decisions.md` append-only
- name direct proof for every behavior claim
- do not close a claim with surrogate proof
- do not update `SYSTEM.md` before direct proof

## Main shift

Do not ask only:

- does the code look plausible?
- do the tests pass?

Also ask:

- what behavior is claimed?
- what exact test or command proves it?
- how could this still be broken while the tests pass?

## If told "start from the roadmap"

1. Read `ROADMAP.md`.
2. Pick one meaningful task.
3. Turn it into `spec-diff.md`.
4. Name the behavior claims.
5. Name the direct proof for each claim.
6. Then write `plan.md`.

## If told "run autonomously"

- propose a small slice stack
- get approval for the stack
- make sure each slice has a proof surface
- run the normal loop per slice
- stop when human judgment is needed

## Default files

```text
.intent/
  SYSTEM.md
  phases/
    001-phase-name/
      spec-diff.md
      plan.md
      reviews_and_decisions.md
      commits.txt
```

## Quick state machine

Session A:

- no phase: create one
- no spec: write claims and proof
- no plan: write proof plan and build plan
- no review: stop for Session B
- no implementation: implement
- no direct proof: keep working
- direct proof exists: update `SYSTEM.md` and `commits.txt`

Session B:

- no spec review: review claims and proof
- else no plan review: review the proof plan
- else review code and evidence
