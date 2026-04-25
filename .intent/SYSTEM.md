# IDD System

This repo codifies a small, text-first version of Intent-Driven
Development for humans and LLMs.

## Current baseline

- The repo currently contains:
  - a human-facing `README.md`
  - `START_HERE.md`
  - `SESSION_A.md`
  - `SESSION_B.md`
  - this `.intent/SYSTEM.md`
  - templates in `.intent/templates/`
- The repo does not currently include automation or custom tooling.
- The repo is intentionally text-first and process-light.

## Purpose

- Preserve intent as a human-owned English baseline.
- Make meaningful changes explicit before code is written.
- Separate critique from response so reviews do not get laundered into
  agreement.
- Give agents a small set of artifacts they can reason about reliably.

## Artifact boundaries

- `SYSTEM.md` is the current proved English model of the system.
  It is normative baseline, not future desire.
- `spec-diff.md` is the intended semantic change for one phase.
- `plan.md` is implementation reasoning.
  It may flag ambiguity, but it must not silently redefine intent.
- `reviews_and_decisions.md` is append-only by round.
  Review rounds record critique.
  Decision rounds record responses.
- `commits.txt` ties the phase to actual commits and evidence.
- A worked example phase may live under `.intent/phases/000-.../`.
  It is instructional scaffolding, not project history.
- `ROADMAP.md` is optional but useful.
  It is for future direction and prioritization, not current truth.
- `CHANGELOG.md` is optional but useful.
  It summarizes what landed after acceptance, but it is not the system
  baseline.

## Session split

- Session A owns:
  - baseline checks
  - spec diff drafting
  - planning
  - implementation
  - evidence gathering
  - responses to review findings
- Session B owns:
  - plan review
  - implementation review
  - follow-up review rounds
- Session B should be a different session from Session A.
- Prefer a different model family for Session B when possible.

## Review rules

- Review against the spec diff.
- Use three reads:
  - positive conformance
  - negative conformance
  - adversarial review
- Name the artifacts reviewed and the evidence reviewed when that adds
  clarity.
- Give findings stable IDs like `P1`, `N1`, `A1`.
- Reference those IDs in decisions.
- Do not rewrite old review text to make it look resolved.
  Append a decision round instead.

## Plan rules

- The best plans usually contain:
  - goal
  - mapping from spec diff to implementation
  - proposed approach
  - tests and evidence
  - files likely to change
  - areas that should not be touched
  - assumptions and risks
- Optional sections like `Context`, `References`, `Traps`,
  `Acceptance`, and `Commands` are good when the phase is complex.
- Do not require those sections for every tiny phase.

## Update rules

- Do not update `SYSTEM.md` just because code exists.
- Update `SYSTEM.md` only after the implementation proves against the
  verification criteria that it deserves to become the new baseline.
- Update `ROADMAP.md` when future direction changes.
- Update `CHANGELOG.md` when an accepted phase lands and should be
  summarized for humans.
- If a change is too large to review cleanly, split the phase instead of
  asking for a more heroic review.

## Non-goals

- This repo does not try to replace taste or judgment.
- This repo does not assume big-team process.
- This repo does not assume heavy tooling is necessary.
- This repo should not grow artifacts unless they clearly reduce
  ambiguity.
