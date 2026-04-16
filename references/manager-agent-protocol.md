# Manager-Agent Protocol

## First Principle

Do not start with role routing.
Start with task-mode classification.

The order is:

1. classify governance strength
2. choose the owner
3. choose advisors if needed
4. separate Brain, Hands, and Review

## Layer Model

- `Brain`: judgment, tradeoffs, escalation decisions, and success criteria
- `Hands`: execution contracts, state transitions, retries, permissions, and failure handling
- `Review`: verification, blockers, residual risk, and comparison against the intended target

These layers should not collapse into one free-form answer on larger tasks.

## Brain

Brain is usually the owner role.

Brain decides:

- what the task is really trying to achieve
- which mode applies
- what success looks like
- which role should own the decision
- whether advisors are needed
- whether stronger review or audit is required

Brain should not:

- absorb raw shell noise
- manage low-level retries
- narrate tool chatter
- impersonate every specialist at once

## Hands

Hands is the execution layer.
Hands does not change goals.
Hands runs contracts.

Every Hands action should be expressible as:

```markdown
Task:
Input:
Allowed Write Scope:
Tools:
Expected Output:
Validation:
Failure Codes:
Retry Policy:
```

Recommended failure codes:

- `blocked-by-permission`
- `blocked-by-missing-context`
- `tool-timeout`
- `tool-flake-retried`
- `validation-failed`
- `unsafe-scope`
- `needs-brain-decision`

Hands may retry tool-level failures.
Hands may not silently change the task objective.

## Review

Review proves the state of the work.
It is not a narrative epilogue.

Review should answer:

- what was actually validated
- what failed
- what remains unresolved
- what residual risk remains
- whether escalation is needed

If the task is in A/B mode, Review must also state whether the candidate passed the gate.

## State Discipline

State is not free-form prose.
Use fixed slots:

- `Input`
- `Completed Actions`
- `Current Blocker`
- `Outputs`
- `Waiting On`
- `Residual Risks`

If the task is large, update State instead of rewriting it from scratch.

## Mode Interaction

### quick

- lightweight governance
- minimal Review
- no heavy Hands contract unless execution is non-trivial

### managed

- one owner
- 0-2 advisors
- explicit Brain / Action / State / Review
- Hands contract when execution matters

### package

- full Brain / Hands / Review split
- round tracking
- verification block
- blocker block
- artifacts block
- audit block for high-risk work

## Security and Control

Safety belongs to execution control, not to optimistic planning.

- use least privilege by default
- keep write scopes explicit
- do not hide irreversible actions
- do not let Brain confidence override permission boundaries

## Observability

At minimum, track:

- whether the user got a fast useful status update
- whether the task reached end-to-end completion
- what class of failure stopped progress

For package mode, also track:

- what round the work is in
- what validations ran
- whether blockers are waiting on the user or on the system

## Partner-Skill Boundary

`partner-skill` governs these layers.
It does not become the layer itself for domain work.

- owner roles provide the domain judgment
- partner provides the governance frame
