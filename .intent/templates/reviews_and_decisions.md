# Reviews And Decisions

This file is append-only.

- Review rounds are written in Session B.
- Prefer a different model family from Session A when possible.
- Decision rounds are written in Session A in response to findings.
- Do not rewrite earlier review text to make it look resolved.

## Review Round 001

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

- [P1] ...

### Negative conformance review

- [N1] ...

### Adversarial review

- [A1] ...

### Review verdict

- ...

## Decision Round 001

Responding to:
- Review Round 001

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

## Review Round 002

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

- [P2] ...

### Negative conformance review

- [N2] ...

### Adversarial review

- [A2] ...

### Review verdict

- ...

## Decision Round 002

Responding to:
- Review Round 002

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

## Notes

- Keep earlier review text intact.
- Add new rounds instead of rewriting history.
- If a finding is addressed later, reference its ID in the decision
  round instead of editing the finding itself.
