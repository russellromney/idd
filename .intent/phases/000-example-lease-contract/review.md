# Review

Phase:
- 000-example-lease-contract

## Execution Review 1

### What looks right

- The phase is narrow.
- The contract is stated in plain English.
- The execute plan says what will not change.

### Proof gaps

- The direct proof should explicitly pin expired-renew behavior.
- The direct proof should include multi-connection access, not just one
  connection.

### Blast-radius gaps

- Make sure release preserves fencing continuity.
- Make sure inspect means "live lease now", not raw row read.

### How this could still be broken

- A single-connection plan could miss shared-file drift.
- Release semantics could still quietly break fencing continuity.

### Open questions

- None after the plan clarifies release and inspect semantics.

### Verdict

- needs execution changes

## Implementation Review 1

### What looks right

- The implementation should stay narrow.
- The tests should prove the core lease transitions before any binding
  exists.

### Proof gaps

- A single-connection suite could pass while shared-file access still
  drifts.
- Release could accidentally delete the row and reset fencing state.

### Blast-radius gaps

- Release must preserve fencing continuity.
- Inspect must stay time-aware.

### How this could still be broken

- needs stronger proof

### Open questions

- None if the tests pin the missing behaviors.

### Verdict

- needs stronger proof
