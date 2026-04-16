# Task-Mode Classification

## Purpose

This file defines the first decision `partner-skill` should make:

How much governance strength does this task deserve?

## Modes

### quick

Use quick mode when all of the following are mostly true:

- one owner is enough
- the task is short-lived
- the process is simple
- verification is lightweight
- no multi-round control loop is needed

Typical examples:

- a short product judgment
- one implementation recommendation
- one narrow routing choice

### managed

Use managed mode when any of the following are true:

- the task needs one owner plus advisory input
- the task needs explicit state tracking
- the task has meaningful execution or review risk
- the task needs more than a quick answer but not a full package

Typical examples:

- choosing one owner and one advisor for a mixed task
- coordinating an implementation plus one review loop
- judging whether a new workflow is strong enough to keep

### package

Use package mode when any of the following are true:

- the task is long-running
- the task is high-investment
- the task spans multiple workstreams
- the task needs repeated review rounds
- blocker management must be explicit
- artifacts must be tracked
- failure recovery matters

Typical examples:

- large refactor plus tests plus docs
- rollout preparation with validation and review
- protocol redesign with trial run and acceptance gate

## Escalation Rule

If you are unsure between two modes, choose the stronger one when:

- the cost of under-governing the task is high
- the task touches safety, permissions, irreversible actions, or public release

Otherwise choose the lighter mode.

## De-Escalation Rule

If the task was initially classified as package but turns out to be much smaller:

- state the change explicitly
- downgrade to managed or quick
- do not keep package overhead just because it was selected first

## Decision Questions

Ask these questions mentally before choosing the mode:

1. How much coordination is actually needed?
2. How costly is failure or drift?
3. Does the task need visible state?
4. Does the task need more than one review cycle?
5. Will the user care about artifacts, blockers, or auditability?

## Output Mapping

- `quick` -> `Goal / Action / Risk / Done`
- `managed` -> `Brain / Action / State / Review`
- `package` -> `Brain / Action / State / Review / Round Status / Verification / Open Blockers / Artifacts`

Add `Audit` for high-risk tasks.
