# Planning Durable State Changes

Use this guide when a bug can lose data, attach data to the wrong owner,
report false recovery, or leave an operation impossible to retry.

Common examples:

- database creation and recovery
- filesystem publication
- object-store uploads
- migrations
- leader or owner changes
- checkpoint and replication boundaries
- work that spans a database and the filesystem

The goal is not more process. The goal is to find the bad states before
implementation turns them into review rounds.

## The pre-code gate

Do not implement until `execute.md` contains:

1. the durability invariants
2. the complete state-transition table
3. ownership rules for every destructive action
4. crash points and retry behavior
5. a proof row for every meaningful transition

If a transition has no declared result, the design is not ready.

## 1. State the invariants

Write short claims that remain true across success, failure, crash, and
retry.

Good durability invariants usually include:

- Unknown or mismatched state causes an error without mutation.
- Code deletes only artifacts that it can prove it owns.
- Success means every required durable component exists and agrees.
- Failure never turns missing or unreadable data into empty data.
- Retrying the same request reaches the same result.
- An ambiguous write is resolved by inspecting durable identity, not by
  guessing whether it succeeded.
- A live operation stops before commit if its required durable state has
  disappeared or changed.
- One component owns each durable transition.
- Alternate paths, aliases, and symlinks cannot bypass ownership or
  locking.

Make each invariant testable. "Be crash safe" is not an invariant.

## 2. Enumerate the state space

List each independent dimension of durable state. Do not start with the
happy-path sequence alone.

Example:

| Dimension | Possible states |
|---|---|
| durable identity | absent, pending same ID, pending different ID, active same ID, active different ID, corrupt |
| primary data | absent, valid same ID, valid different ID, corrupt, unknown file, alias or symlink |
| supporting storage | absent, complete, partially missing, wrong owner |
| request | create, retry create, restore, retry restore, ordinary open, live mutation |
| interruption | before and after each write, sync, rename, commit, and external call |

Then write the transition table. Each meaningful row gets exactly one
outcome:

- succeed with the requested durable identity
- resume the same operation
- fail without mutation

Do not use "best effort," "probably incomplete," or "clean it up" as an
outcome. State how ownership is proved and what exact bytes may change.

## 3. Prove ownership before cleanup

Unreadable does not mean disposable.

Safe cleanup requires positive ownership evidence, such as:

- an exclusively created temporary path containing the request ID
- a durable marker written by this operation
- a database identity that was read and matched successfully

An open error, parse error, missing identity, unexpected schema, or
corrupt file is not ownership evidence. Preserve the artifact and return
the error.

Prefer protocols that make ownership obvious. For example:

1. persist a pending request ID
2. create at an exclusive temporary path tied to that ID
3. initialize and sync the temporary artifact
4. initialize and sync supporting storage
5. atomically publish the artifact
6. sync its parent
7. mark the request active last

Only the ID-qualified temporary artifact is automatically disposable.
Unknown files at the final path are never deleted.

## 4. Design retry before success

For every durable step, ask:

> What does the next process observe if this step completed but its caller
> received an error?

This matters after rename, commit, remote acknowledgement, and directory
sync. The caller may not know whether the operation happened.

A good retry reads durable identity and converges:

- pending plus an owned temporary artifact resumes
- pending plus a valid matching published artifact finishes activation
- active plus the same valid artifact returns success
- different, corrupt, or unknown state fails without mutation

Do not make a successful-but-ambiguously-reported operation impossible to
retry.

## 5. Keep lifecycle authority narrow

The component that knows the full protocol should own its ordering.

Avoid public APIs that let ordinary callers:

- publish before initialization is durable
- activate before data is durable
- clean up an artifact without ownership proof
- recreate required state during an ordinary reopen

Prefer returning an already-active handle over exposing loosely ordered
`prepare()`, `publish()`, and `activate()` calls. Use additional abstraction
only when it makes invalid ordering impossible or materially clearer.

## 6. Write the proof matrix first

Every transition row needs executable proof. Use two layers.

### User-shaped proof

Exercise the real public path and assert the observable result:

- create, write, stop, reopen, read exact bytes
- fail and retry with the same request ID
- restore a complete matching state
- refuse foreign, corrupt, mismatched, aliased, or incomplete state
- lose a required component while live and prove the next mutation does
  not commit

For every negative test, capture before and after state. Compare primary
data, identity records, supporting files, directory layout, and externally
visible head or revision.

### Fault-injection proof

User-shaped tests cannot reliably hit every crash boundary. Add failpoints
before and after each:

- file write
- file sync
- rename
- parent-directory sync
- database commit
- durable activation
- external acknowledgement

After each injected failure, restart and repeat the same request. Assert
that it reaches the exact intended state or fails without mutation.

Kill mutants for load-bearing refusal paths. In particular, prove tests
fail if code:

- swallows an identity error
- deletes an unknown artifact
- recreates missing active storage
- skips active identity validation
- treats an ambiguous result as a different request

## 7. Prove the blast radius

Durability work often changes shared storage, locking, or open behavior.
List old operations that share those paths and rerun their user-shaped
flows.

Include at least:

- ordinary open and close
- read and write
- restart
- deletion and cleanup
- concurrency or exclusivity
- restore or migration, when present

Passing the new recovery test is not enough if ordinary reads can now open
the wrong data or cleanup can remove a shared artifact.

## 8. Review in this order

Session B reviews durable work in this order:

1. Are the invariants complete and testable?
2. Does every meaningful state combination have a declared outcome?
3. Is every destructive action backed by positive ownership evidence?
4. Can every ambiguous failure be retried safely?
5. Does every transition have direct positive or negative proof?
6. Do the tests fail when the dangerous guard is removed?
7. Does blast-radius proof cover shared paths?
8. Only then: does the implementation match the approved protocol?

If review discovers a missing state class, stop patching individual
symptoms. Add the class to the transition table, extend the proof matrix,
and review the protocol again before changing code.

## Copy into execute.md

```markdown
## Durability invariants

- ...

## Durable state dimensions

| Dimension | States |
|---|---|
| ... | ... |

## Transition table

| Existing state | Request | Expected result | Allowed mutation | Retry result | Proof |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

## Ownership and cleanup

- Artifact:
- Ownership evidence:
- Safe cleanup rule:
- Unknown-state behavior:

## Crash points

| Failure point | Durable state afterward | Same-request retry | Proof |
|---|---|---|---|
| ... | ... | ... | ... |

## User-shaped proof

- positive:
- negative:
- exact before/after assertions:

## Fault-injection proof

- ...

## Blast-radius proof

- ...
```

