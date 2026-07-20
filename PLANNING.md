# Planning Before Implementation

Use this guide to make a phase ready for execution.

The point is not more planning text. The point is to find missing product
and design decisions before code turns them into repeated review rounds.

A one-line change does not need this machinery. Use it when a phase adds a
capability, changes a lifecycle, joins multiple components, introduces a
new abstraction, or carries meaningful correctness risk.

## The pre-code gate

Do not implement a substantial phase until another engineer can answer:

1. What can the user do when this is complete?
2. What are the meaningful states, operations, and boundaries?
3. What happens for invalid, repeated, stale, conflicting, and partial
   requests?
4. What must never happen?
5. Which component owns each decision and transition?
6. What existing behavior must remain unchanged?
7. What is explicitly out of scope?
8. Why is this the simplest design that meets the intent?
9. Which realistic positive and negative tests prove each claim?
10. Which decisions still need a human answer?

If the implementer must invent product behavior to proceed, the plan is
not ready.

## 1. Start with the user outcome

Describe the capability in concrete terms:

- who uses it
- what they do
- what they observe on success
- what they observe on refusal or failure
- what remains true afterward

Prefer a short user-shaped example over an internal feature label.

Weak:

> Add namespace lifecycle support.

Stronger:

> A caller creates a namespace with one manifest database ID, writes data,
> closes it, and reopens the same bytes. Attempts to attach a different
> manifest database fail without changing either namespace.

The example does not replace the detailed contract. It gives the rest of
the plan something concrete to preserve.

## 2. Draw the system boundary

Name the pieces involved and what each one owns.

For each component, state:

- the data or decision it owns
- the interface other components use
- what it must not decide
- which existing paths share it

Call out the source of truth. If two stores, services, or files can
disagree, say which one wins and how disagreement is handled.

This is also where misplaced abstractions become visible. A storage layer
should not quietly own product lifecycle policy. A router should not own
business rules. A generic helper should not expose ordering that only one
coordinator can use safely.

## 3. Describe the whole lifecycle

Do not plan only the new happy-path operation. Follow the thing through its
life:

- creation or first use
- ordinary use
- repeated and concurrent requests
- update or replacement
- close and restart
- recovery or retry
- deletion and cleanup

Not every phase needs every step. Mark irrelevant steps explicitly so the
reader knows they were considered rather than forgotten.

For each relevant step, name the preconditions, visible result, state
change, and refusal behavior.

## 4. State invariants, non-changes, and non-goals

An invariant is a testable sentence that must remain true across all
operations.

Good examples:

- A historical read never advances the current revision.
- A failed rename leaves both paths unchanged.
- A namespace accepts only its bound manifest database ID.
- Cloud synchronization does not change local write semantics.

Also list what must not change. This defines the blast radius and prevents
the implementation from improving unrelated code.

List non-goals separately. A non-goal is not permission to leave adjacent
behavior ambiguous. State what happens at the boundary even when the full
capability is deferred.

## 5. Enumerate behavior, not anecdotes

When behavior depends on state or input combinations, write a decision or
transition table.

Useful dimensions include:

- resource state: absent, valid, stale, partial, corrupt, deleted
- identity: same, different, missing, malformed
- request: first, repeated, conflicting, concurrent
- mode or configuration: each supported value, disabled, invalid
- authority: allowed, denied, expired
- dependency result: success, refusal, timeout, ambiguous completion

Each meaningful row needs one declared outcome:

- succeed and produce an exact result
- return an existing result without change
- retry or resume
- fail without mutation

Do not enumerate a Cartesian product for ceremony. Combine equivalent
rows. The goal is to expose different behavior classes, especially the
ones the happy path hides.

## 6. Resolve product semantics explicitly

Plans often fail because small-looking decisions are left to the
implementer:

- Does repeating the same request succeed or conflict?
- Is an operation a no-op or does it create a revision?
- Does "durable" mean local disk or remote storage?
- What is the default mode?
- Which settings are knobs, and which are invariants?
- What is the stable user-facing name?
- What does an empty, missing, or unknown value mean?

Write the answer in product terms. Do not let fixtures, schemas, or helper
APIs choose semantics accidentally.

Put unresolved choices in an explicit decision list. Stop execution only
for choices that materially change the product or architecture. Resolve
the rest during planning and record the judgment.

## 7. Set a complexity budget

Explain why each new mechanism earns its cost.

Ask:

- Can a transaction or existing primitive provide the guarantee?
- Can one owner perform the complete operation?
- Does a new trait have more than one real implementation?
- Does a new state table represent product state or compensate for a weak
  API?
- Can invalid ordering be removed instead of documented?
- Are background workers, triggers, audit rows, or coordination layers
  required by the user intent?
- Is an optimization being mistaken for a first-version requirement?

Prefer the smallest design whose guarantees are easy to explain and test.
Do not remove necessary state merely to reduce line count. Do not add
machinery for a hypothetical future.

Name known awkwardness in the plan. A staff engineer should be able to see
where the design may need to evolve without discovering hidden complexity
in the implementation.

## 8. Plan failure and retry where they exist

If the work crosses processes, transactions, files, services, or durable
steps, describe failure as part of the normal protocol.

For each destructive action, state the positive evidence that authorizes
it. Unreadable, missing, corrupt, or unexpected state is not proof that an
artifact is safe to delete.

For each commit, rename, sync, message, or external acknowledgement, ask:

> What does the next attempt observe if this completed but the caller
> received an error?

The plan must define how the same request resolves that ambiguity. It must
not silently create empty state, attach the wrong identity, repeat a
non-idempotent action, or make a successful operation impossible to retry.

For crash-sensitive work, add a state-transition table with:

| Existing state | Request | Expected result | Allowed mutation | Retry result | Proof |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

This section is conditional. Do not force crash-consistency machinery onto
work that has no durable or distributed transition.

## 9. Build the proof matrix before code

Map every important claim to executable proof.

Use the strongest relevant level:

- unit proof for local rules
- integration proof for component boundaries
- user-shaped e2e proof for visible behavior
- adversarial proof for risky refusals and failure paths
- blast-radius proof for old behavior sharing changed code

Positive and negative tests should exercise the same real entry points a
user or caller uses. Helper tests alone are surrogate proof.

For negative behavior, assert both parts:

1. the operation returned the promised error
2. the protected state did not change

For risky guards, prove the test itself: disable or mutate the guard and
watch the relevant test fail.

When deterministic failures cannot be produced through the public path,
use focused failpoints underneath a realistic integration flow. Fault
injection complements user-shaped proof; it does not replace it.

A useful proof table is:

| Claim | Risk if wrong | Direct proof | Negative proof | Blast-radius proof |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

## 10. Sequence the implementation around proof

Split work where a boundary can be completed and proved independently.
Do not split it so an intermediate phase knowingly permits corruption,
false success, or two competing sources of truth.

Each phase should leave the repository in a coherent state and say:

- what becomes real in this phase
- what remains on the old path
- how the boundary between them works
- what later work may assume
- what later work must not assume

Put deferred work in a register with its risk, trigger, and suggested next
step. Nothing disappears because it was inconvenient during execution.

## 11. Stop the review loop

When review finds one missed example, ask whether it represents a whole
missing class.

Examples:

- one retry bug may mean retry semantics were never designed
- one wrong-identity bug may mean ownership was never defined
- one untested error may mean negative proof is missing for an operation
  family
- one awkward wrapper may mean responsibility sits in the wrong layer

If a class is missing:

1. stop patching the individual symptom
2. add the missing dimension to the plan
3. enumerate the whole class
4. update the behavior and proof matrices
5. review the revised design
6. then resume implementation

Do not send the same implementation back through review with only the last
example fixed. That turns review into serial design discovery.

## 12. Review the plan before the implementation

Session B reviews in this order:

1. Is the user outcome concrete?
2. Are ownership and system boundaries clear?
3. Is the whole relevant lifecycle covered?
4. Are invariants and non-changes testable?
5. Are all distinct behavior classes specified?
6. Are product semantics and defaults explicit?
7. Does each mechanism earn its complexity?
8. Are failure, retry, and cleanup defined where relevant?
9. Does every important claim have realistic positive and negative proof?
10. Does blast-radius proof cover shared paths?
11. Are unresolved decisions visible?

Only after those questions pass should implementation review begin.

## Copy into execute.md

Use only the sections the phase needs.

```markdown
# Outcome

## User-shaped examples

## System boundary and ownership

## Lifecycle

## Invariants

## What will not change

## Non-goals

## Behavior matrix

| Existing state or input | Operation | Result | State change | Proof |
|---|---|---|---|---|
| ... | ... | ... | ... | ... |

## Product decisions

## Simplest design

## Failure, retry, and cleanup

## Implementation sequence

## Proof matrix

| Claim | Direct proof | Negative proof | Blast-radius proof |
|---|---|---|---|
| ... | ... | ... | ... |

## Deferred work

## Open decisions
```
