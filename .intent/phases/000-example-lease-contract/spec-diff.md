# Spec Diff

Phase:
- 000-example-lease-contract

Session:
- A

## What changes

- The system gains a small SQLite-backed lease contract for named
  resources.
- The core contract supports `inspect`, `claim`, `renew`, and `release`.
- A monotonic fencing token is introduced for each resource.

## What does not change

- The system does not become distributed consensus.
- The system does not add waiting queues or fairness guarantees.
- No language binding is required in this phase.

## How we will verify it

- A resource can be claimed and later inspected as live.
- A second claimant cannot take a still-live lease.
- An expired lease can be taken over and increments the fencing token.
- Only the current owner can renew or release a live lease.
- The contract is proven with tests before any binding depends on it.

## Notes

- This is a worked example phase for the IDD repo.
- It exists to demonstrate artifact shape, not to represent this repo's
  own product history.

