# Start Here

Use this when a session is told:

> look at `../idd` and init here

## Order

1. Read this file.
2. Decide if you are writing the plan or reviewing it.
3. Read the matching card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)
4. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md)
   only if you need more context.

## Hard rules

- do not implement from `ROADMAP.md`
- keep `SYSTEM.md` honest
- write `plan.md` in plain English
- make proof explicit before coding
- prefer user-shaped e2e for changed behavior
- prove blast radius, not just the new path

## If told "start from the roadmap"

1. Read `ROADMAP.md`.
2. Pick one meaningful task.
3. Write `plan.md`.
4. Include:
   - what we are building
   - what will not change
   - how we will prove the new behavior
   - how we will prove old behavior still holds
5. Then get review.

## Default files

```text
.intent/
  SYSTEM.md
  phases/
    001-phase-name/
      plan.md
      review.md
      commits.txt
```
