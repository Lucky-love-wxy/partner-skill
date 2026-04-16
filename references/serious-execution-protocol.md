# Serious Execution Protocol

## Purpose

This protocol is for `package` mode.
Use it when the task is too important, too long, too cross-cutting, or too failure-prone for lightweight coordination.

## Trigger Signals

Escalate to package mode when the user says things like:

- this is a large task
- execute fully
- do not stop at one step
- end-to-end
- investigation + change + verification
- two review rounds
- keep going until it is done

Also escalate when the task itself implies:

- multiple workstreams
- code plus tests plus documentation
- long-running execution
- visible blocker management
- repeated review loops

## Package Defaults

A package-mode task assumes the workflow may include:

- implementation
- tests
- CI or build repair
- documentation updates
- review loops
- artifact tracking

Do not only perform the most convenient slice if the rest is likely to become a blocker.

## Required Output Blocks

Package mode must include:

- `Brain`
- `Action`
- `State`
- `Review`
- `Round Status`
- `Verification`
- `Open Blockers`
- `Artifacts`

Add `Audit` for high-risk work.

## Round Structure

### Round 1

- read the relevant code and task context
- implement or investigate
- run validation
- perform the first strict review

### Round 2

- fix review findings
- rerun validation
- perform the second review

### Round 3+

Continue if:

- high-priority blockers remain
- validation still fails
- review still finds issues

Stop only when:

- blockers are cleared
- the remaining decision belongs to the user
- or there is an explicit objective reason validation cannot continue

## Hands Discipline

Package mode should use Hands contracts by default.

If a Hands contract is not needed, say why explicitly.

## Verification Discipline

Every package-mode task should make verification visible.

Minimum checks when relevant:

- build
- test
- lint
- manual confirmation when automation is not enough

If validation cannot run:

- explain why
- state what substitute check was used
- record the residual risk in `State` and `Review`

## Artifact Discipline

Artifacts are not just files.
Artifacts may include:

- changed code
- reports
- generated docs
- evaluation tables
- screenshots
- release notes

List them explicitly in `Artifacts`.

## Audit Upgrade

If the task is high-risk, package mode must append an `Audit` block.
See `audit-protocol.md`.
