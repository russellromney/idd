# Reviews And Decisions

This file is append-only.

## Review Round 001

Target:
- plan review

Session:
- B

Model family:
- different from Session A when possible

Artifacts reviewed:
- `spec-diff.md`
- `plan.md`

Verification reviewed:
- planned test matrix only

### Positive conformance review

- [P1] The plan keeps the phase narrow and aligned with the spec diff.
- [P2] The plan wisely stops at the core contract and tests before
  adding bindings.

### Negative conformance review

- [N1] The plan flags release semantics as ambiguous, but the phase
  needs a concrete decision before implementation.
- [N2] The plan flags `inspect` ambiguity, but the product question is
  explicitly "who owns this right now?", which argues for live-lease
  semantics.

### Adversarial review

- [A1] This becomes dumb if it is just a named lock with a TTL and a new
  noun.
- [A2] This becomes misleading if it overclaims "leader election" before
  fencing continuity is proven.

### Review verdict

- Accepted with follow-up decisions required before coding.

## Decision Round 001

Responding to:
- Review Round 001

Session:
- A

### Inputs

- [P1]
- [P2]
- [N1]
- [N2]
- [A1]
- [A2]

### Decisions

- [D1] Accept [N1]
  Action: make release preserve the row and clear ownership instead of
  deleting the row.
  Targets: `plan.md`

- [D2] Accept [N2]
  Action: define `inspect` as a live-lease read rather than a raw row
  read.
  Targets: `plan.md`

- [D3] Accept [A1]
  Action: keep the scope at lease state, expiry, fencing, and tests.
  Targets: implementation scope

- [D4] Accept [A2]
  Action: do not market or document the example as a full leader
  election system.
  Targets: docs language

### Verification

- `plan.md` now contains the accepted clarifications

### Decision verdict

- Ready for implementation.

## Review Round 002

Target:
- implementation review

Session:
- B

Model family:
- different from Session A when possible

Artifacts reviewed:
- `spec-diff.md`
- `plan.md`
- core implementation
- tests

Verification reviewed:
- `cargo test`

### Positive conformance review

- [P3] The implementation matches the clarified plan closely.
- [P4] The tests prove the main lease transitions before any binding
  exists.

### Negative conformance review

- [N3] The initial test suite does not explicitly pin expired-renew
  behavior yet.
- [N4] The initial tests are all single-connection tests and do not yet
  prove shared-file multi-connection behavior.

### Adversarial review

- [A3] The next real hardening step is not more mutation code.
  It is proving realistic multi-connection access and teaching future
  callers how to use fencing tokens correctly.

### Review verdict

- Accepted with follow-up test hardening.

## Decision Round 002

Responding to:
- Review Round 002

Session:
- A

### Inputs

- [P3]
- [P4]
- [N3]
- [N4]
- [A3]

### Decisions

- [D5] Accept [N3]
  Action: add an explicit expired-renew test.
  Targets: tests

- [D6] Accept [N4]
  Action: add shared-file multi-connection tests.
  Targets: tests

- [D7] Defer [A3]
  Action: keep future fencing-token usage guidance for a later phase or
  downstream wrapper docs.
  Targets: future work

### Verification

- `cargo test` passes after the follow-up tests land

### Decision verdict

- Phase accepted at the example-core level.

## Notes

- This example shows the intended separation:
  Session A plans, codes, and responds.
  Session B reviews.
- Findings stay stable and are referenced by later decisions.
- The review text is preserved even after responses are made.

