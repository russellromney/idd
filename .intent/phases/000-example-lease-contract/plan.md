# Plan

Phase:
- 000-example-lease-contract

Session:
- A

## Goal

Build the smallest useful lease contract first, before any binding
surface exists.

## Context

- The intent is a single-machine SQLite lease primitive.
- The phase should prove semantics in the core layer before wrapping
  them.

## References

- `.intent/SYSTEM.md`
- `.intent/phases/000-example-lease-contract/spec-diff.md`

## Mapping from spec diff to implementation

1. one durable row shape for resource lease state
2. one schema bootstrap function
3. one core API for lease transitions
4. one test suite that proves the transitions match the diff

## Phase decisions

- resource state lives in one table
- resource rows persist after first claim so fencing stays monotonic
- `inspect` is time-aware and returns only a live lease
- release clears ownership but preserves fencing state
- the phase stops at core code and tests

## Proposed implementation approach

- define the lease types and result shapes first
- bootstrap the schema next
- implement `inspect` before mutation operations
- implement `claim`, then `renew`, then `release`

## Build order

1. types and errors
2. schema bootstrap
3. `inspect`
4. `claim`
5. `renew`
6. `release`
7. tests

## Acceptance

- one current owner per named resource
- expiry is durable and inspectable
- fencing token increments on successful claim
- released resources do not lose their fencing token

## Tests and evidence

- bootstrap is idempotent
- absent resources inspect as `None`
- expired resources inspect as `None`
- first claim succeeds
- second live claim is rejected
- expired takeover succeeds
- renew succeeds only for current live owner
- release succeeds only for current live owner

## Traps

- deleting rows on release would break fencing continuity
- a non-time-aware `inspect` would quietly drift from the intended
  product meaning
- adding a binding too early would calcify convenience APIs before core
  semantics settle

## Files likely to change

- core crate source
- tests
- crate manifest

## Areas that should not be touched

- scheduler behavior
- distributed coordination stories
- language bindings

## Assumptions and risks

- core lease semantics are easier to stabilize than binding ergonomics
- review may force clarification of release or inspection semantics

## Commands

- `cargo test`

## Ambiguities noticed during planning

- Should release delete the row or preserve it?
- Should `inspect` be raw row inspection or live-lease inspection?

## Notes

- These ambiguities should be resolved by review and decision, not
  silently by planning.

