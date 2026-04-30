# Review

Phase:
- 000-example-lease-contract

## What looks right

- The phase is narrow.
- The contract is stated in plain English.
- The plan says what will not change.
- The tests cover the core lease transitions before any binding exists.

## Proof gaps

- Add an explicit expired-renew test.
- Add multi-connection tests so proof is not limited to one connection.

## Blast-radius gaps

- Make sure release preserves fencing continuity.
- Make sure inspect means "live lease now", not raw row read.

## How this could still be broken

- A single-connection suite could pass while shared-file access still
  drifts.
- Release could accidentally delete the row and reset fencing state.

## Open questions

- None after the plan clarifies release and inspect semantics.

## Verdict

- needs stronger proof
