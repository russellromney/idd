# Start Here

Use this file when a new session is told:

> look at `../idd` and init here

The goal is to orient fast, not to read the whole repo first.

## Bootstrap order

1. Read this file.
2. Read [README.md](/Users/russellromney/Documents/Github/idd/README.md) for
   the human explanation if you need more context.
3. Read [.intent/SYSTEM.md](/Users/russellromney/Documents/Github/idd/.intent/SYSTEM.md)
   for the normative process rules.
4. Decide whether you are Session A or Session B.
5. Read the matching role card:
   - [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md)
   - [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md)

## If the instruction is "start from the first roadmap task"

Use this interpretation:

- read the target repo's `ROADMAP.md`
- pick the first real task that should become a meaningful phase
- do not implement directly from the roadmap
- turn that roadmap item into a `spec-diff.md`
- then write `plan.md`

The roadmap is not enough on its own. It motivates a phase, but it does
not replace the phase artifacts.

## Choose your session

### Session A

You own:

- baseline check
- `spec-diff.md`
- `plan.md`
- implementation
- evidence gathering
- responses to review findings

Start with [SESSION_A.md](/Users/russellromney/Documents/Github/idd/SESSION_A.md).

### Session B

You own:

- plan review
- implementation review
- follow-up review rounds

Start with [SESSION_B.md](/Users/russellromney/Documents/Github/idd/SESSION_B.md).

Prefer a different model family from Session A when possible.

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

## Fast rules

- `SYSTEM.md` is current baseline, not aspiration
- roadmap is upstream, changelog is downstream
- plan is implementation reasoning, not new intent
- review against the spec diff
- use `reviews_and_decisions.md`, not ad hoc review filenames
- do not rewrite old review text to make it look resolved
- update `SYSTEM.md` only after proof

