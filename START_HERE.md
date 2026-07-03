# Start Here

Use this when a session is told:

> look at `../idd` and init here

## Order

1. Read this file.
2. Write or review?
3. Read the matching card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)
4. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md)
   only if you need more context.

## Hard rules

- do not implement from `ROADMAP.md`
- write `execute.md` in plain English
- keep `review.md` append-only
- make proof explicit before coding
- prefer user-shaped e2e for changed behavior
- prove blast radius, not just the new path
- no phase names or artifact names in code

## If told "start from the roadmap"

1. Read `ROADMAP.md`.
2. Pick one meaningful task.
3. Write `execute.md` with:
   - what we are building
   - what will not change
   - how we will build it
   - how we will prove the new behavior
   - how we will prove old behavior still holds
4. Then get `Execution Review 1` in `review.md`.

## Default files

```text
.intent/
  phases/
    001-phase-name/
      execute.md
      review.md
      commits.txt
```
