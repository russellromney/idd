# Start Here

Use this file when a new session is told:

> look at `../idd` and init here

The goal is to orient fast and start with the right proof standard.

## Bootstrap order

1. Read this file.
2. Determine whether you are Session A or Session B.
   - default to Session A for new work
   - use Session B when explicitly asked to review or audit proof
3. Read the matching role card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)
4. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md)
   only if you need the full process context or are changing the
   process itself.

For most sessions, this file plus one role card should be enough.

## Hard rules

- MUST not implement directly from `ROADMAP.md`
- MUST review against `spec-diff.md`
- MUST keep `reviews_and_decisions.md` append-only
- MUST name direct executable proof for every behavior claim
- MUST not treat surrogate proof as closure
- MUST not update `SYSTEM.md` before direct proof

## The main mindset shift

Do not ask only:

- is the code plausible?
- do the unit tests pass?
- are the artifacts tidy?

Also ask:

- what exact behavior is being claimed?
- what exact test or command directly proves it?
- how could this still be broken while the current tests pass?

If you cannot answer those three questions, the phase is not ready to
be called done.

## If told "start from the first roadmap task"

Use this interpretation:

- read the target repo's `ROADMAP.md`
- pick the first meaningful task that should become one phase
- turn that roadmap item into a `spec-diff.md`
- name the behavior claims
- name the direct proof expected for each claim
- only then write `plan.md`

The roadmap motivates a phase. It does not replace phase artifacts.

## If told "run autonomously" or "run the bucket"

Use Session A's autonomous mode:

- propose a small ordered stack of slices first
- get human approval for the slice shape
- make sure each slice has a concrete proof surface
- run the normal loop per slice
- stop when a semantic or product judgment is needed

Autonomy is fine. Unproved behavior is not.

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

## Quick state machine

If you are Session A:

- if there is no phase yet, create one from the first roadmap task
- if there is no `spec-diff.md`, write behavior claims and proof
  obligations first
- else if there is no `plan.md`, write the proof plan before the build
  plan
- else if review is missing, stop for Session B
- else if implementation is not done, implement
- else if direct proof is still missing, keep working and do not claim
  done
- else update `SYSTEM.md`, `commits.txt`, and optionally
  `CHANGELOG.md`

If you are Session B:

- if `spec-diff.md` exists and has no spec review, review the claims and
  proof obligations
- else if `plan.md` exists and has no plan review, review whether the
  plan can actually produce the proof
- else review implementation and evidence
- in every case, ask how the feature could still be broken while the
  current tests pass
