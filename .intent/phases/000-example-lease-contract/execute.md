# Execute

Phase:
- 000-example-lease-contract

## Notes

- This worked example combines intent and execution in one file.
- In a real phase, the "What we are building" and "What will not change"
  sections belong in `spec-diff.md`.

## What we are building

- A small SQLite-backed lease contract for named resources.
- The contract supports `inspect`, `claim`, `renew`, and `release`.
- Each resource has a monotonic fencing token.

## What will not change

- This does not become distributed consensus.
- This does not add waiting queues or fairness rules.
- This does not add language bindings yet.

## How we will build it

- main code path:
  types -> schema bootstrap -> inspect -> claim -> renew -> release
- key files:
  core crate source and tests
- risky seams:
  release semantics and fencing continuity
- build order:
  1. types and errors
  2. schema bootstrap
  3. inspect
  4. claim
  5. renew
  6. release
  7. tests

## How we will prove it works

- direct proof:
  claim / renew / release behavior matches the intended contract
- unit proof:
  schema bootstrap and transition rules
- integration proof:
  multi-connection tests over one shared SQLite file
- e2e proof:
  not needed in this small core-only example
- adversarial proof:
  expired takeover, invalid renew, invalid release

## How we will prove we did not break earlier intent

- old behavior at risk:
  fencing continuity and live-lease inspection semantics
- regression proof:
  released rows keep fencing state
  expired leases inspect as absent
- blast-radius checks:
  release does not delete rows
  inspect is time-aware

## Commands

- `cargo test`

## Notes

- This is a worked example.
