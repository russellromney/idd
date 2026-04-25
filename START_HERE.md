# Start Here

Use this file when a new session is told:

> look at `../idd` and init here

The goal is to orient fast and start correctly.

## Bootstrap order

1. Read this file.
2. Decide whether you are Session A or Session B.
3. Read the matching role card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)
4. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md) or
   [.intent/SYSTEM.md](/Users/russellromney/Documents/Github/idd/.intent/SYSTEM.md)
   only if you need deeper context or are changing the process itself.

For most sessions, this file plus one role card should be enough.

## Hard rules

- MUST not implement directly from `ROADMAP.md`
- MUST review against `spec-diff.md`
- MUST use `reviews_and_decisions.md`
- MUST keep review text append-only
- MUST not update `SYSTEM.md` before proof

## If told "start from the first roadmap task"

Use this interpretation:

- read the target repo's `ROADMAP.md`
- pick the first real task that should become a meaningful phase
- turn that roadmap item into a `spec-diff.md`
- then write `plan.md`

The roadmap motivates a phase. It does not replace phase artifacts.

## Default artifact set

Use this unless the repo already has a better-established variant:

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

Templates live in
[`/.intent/templates/`](</Users/russellromney/Documents/Github/idd/.intent/templates>).
One worked example lives in
[`/.intent/phases/000-example-lease-contract/`](</Users/russellromney/Documents/Github/idd/.intent/phases/000-example-lease-contract>).

## Quick state machine

If you are Session A:

- if there is no phase yet, create one from the first roadmap task
- if there is no `spec-diff.md`, write it
- else if there is no `plan.md`, write it
- else if there is no review round yet, stop for Session B
- else if decisions are needed, write them
- else if implementation is not done, implement
- else if no implementation review exists, stop for Session B
- else respond to findings
- else update `SYSTEM.md`, `CHANGELOG.md`, and `commits.txt` as needed

If you are Session B:

- if `plan.md` exists and no plan review exists, review the plan
- else if implementation exists and no implementation review exists,
  review the implementation
- else review the latest follow-up changes
