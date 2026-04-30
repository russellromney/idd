# Reviews And Decisions

This file is append-only.

- Review rounds are written in Session B.
- Decision / response rounds are written in Session A.
- Do not rewrite earlier review text to make it look resolved.

## Spec Review 1

Target:
- spec-diff review

Session:
- B

Artifacts reviewed:
- `spec-diff.md`

Verification reviewed:
- ...

### Positive conformance

- [P1] ...

### Negative conformance

- [N1] ...

### Proof audit

- [A1] Claim X has direct proof / only surrogate proof / missing proof

### Review verdict

- ...

## Spec Response 1

Responding to:
- Spec Review 1

Session:
- A

### Inputs

- [P1]
- [N1]
- [A1]

### Decisions

- [D1] ...

### Verification

- ...

### Response verdict

- ...

## Plan Review 1

Target:
- plan review

Session:
- B

Artifacts reviewed:
- `spec-diff.md`
- `plan.md`

Verification reviewed:
- ...

### Positive conformance

- [P2] ...

### Negative conformance

- [N2] ...

### Proof audit

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

- [D2] ...

### Verification

- ...

### Response verdict

- ...

## Implementation Review 1

Target:
- implementation review

Session:
- B

Artifacts reviewed:
- `spec-diff.md`
- `plan.md`
- implementation files
- tests

Verification reviewed:
- ...

### Positive conformance

- [P3] ...

### Negative conformance

- [N3] ...

### Proof audit

- [A3] For each behavior claim, say whether the evidence is direct,
  surrogate, or missing.

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

- [D3] ...

### Verification

- ...

### Response verdict

- ...

## Notes

- Keep earlier review text intact.
- Add new rounds instead of rewriting history.
- If a finding is addressed later, reference its ID in the response
  round instead of editing the finding itself.
- The most important implementation-review question is whether the code
  directly proved the claimed behavior or only proved nearby facts.
