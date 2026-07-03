# Start Here

Use this when a session is told:

> look at `../idd` and init here

## Order

1. Read this file.
2. Decide if you are writing the intent/execution or reviewing it.
3. Read the matching card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)
4. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md)
   only if you need more context.

## Hard rules

- do not implement from `ROADMAP.md`
- write `spec-diff.md` before `execute.md`
- write `execute.md` in plain English
- keep `review.md` append-only
- make proof explicit before coding
- prefer user-shaped e2e for changed behavior
- prove blast radius, not just the new path
- planning artifact names, phase numbers, and phase names stay out of code

## If told "start from the roadmap"

1. Read `ROADMAP.md`.
2. Pick one meaningful task.
3. Write `spec-diff.md`.
4. Include:
   - what we are building
   - what will not change
5. Write `execute.md`.
6. Include:
   - how we will build it
   - how we will prove the new behavior
   - how we will prove old behavior still holds
7. Then get `Execution Review 1` in `review.md`.

## Default files

```text
.intent/
  phases/
    001-phase-name/
      spec-diff.md
      execute.md
      review.md
      commits.txt
```
