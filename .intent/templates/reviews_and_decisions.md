# Reviews And Decisions

This file is append-only.

- Review rounds are written in Session B.
- Prefer a different model family from Session A when possible.
- Decision rounds are written in Session A in response to findings.
- Do not rewrite earlier review text to make it look resolved.

## Intent Review 1

Target:
- spec-diff review

Session:
- B

Model family:
- ...

Artifacts reviewed:
- `spec-diff.md`

Verification reviewed:
- ...

### Positive conformance review

- [P1] ...

### Negative conformance review

- [N1] ...

### Adversarial review

- [A1] ...

### Review verdict

- ...

## Intent Response 1

Responding to:
- Intent Review 1

Session:
- A

### Inputs

- [P1]
- [N1]
- [A1]

### Decisions

- [D1] Accept [N1]
  Action: ...
  Targets: ...

- [D2] Defer [A1]
  Action: ...
  Targets: ...

### Verification

- ...

### Decision verdict

- ...

## Plan Review 1

Target:
- plan review

Session:
- B

Model family:
- ...

Artifacts reviewed:
- `spec-diff.md`
- `plan.md`

Verification reviewed:
- ...

### Positive conformance review

- [P2] ...

### Negative conformance review

- [N2] ...

### Adversarial review

- [A2] ...

### Review verdict

- ...

## Plan Response 1

Responding to:
- Plan Review 1

Session:
- A

### Inputs

- [P2]
- [N2]
- [A2]

### Decisions

- [D3] ...

### Verification

- ...

### Decision verdict

- ...

## Implementation Review 1

Target:
- implementation review

Session:
- B

Model family:
- ...

Artifacts reviewed:
- `spec-diff.md`
- `plan.md`
- implementation files
- tests

Verification reviewed:
- ...

### Positive conformance review

- [P3] ...

### Negative conformance review

- [N3] ...

### Adversarial review

- [A3] ...

### Review verdict

- ...

## Implementation Response 1

Responding to:
- Implementation Review 1

Session:
- A

### Inputs

- [P3]
- [N3]
- [A3]

### Decisions

- [D4] ...

### Verification

- ...

### Decision verdict

- ...

## Notes

- Keep earlier review text intact.
- Add new rounds instead of rewriting history.
- If a finding is addressed later, reference its ID in the decision
  round instead of editing the finding itself.
- Later follow-up rounds should continue the same naming pattern, for
  example `Implementation Review 2` and `Implementation Response 2`.
