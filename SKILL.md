---
name: partner-skill
description: Govern complex multi-role AI work by classifying task mode before routing skills. Use when the first decision should be governance strength rather than domain expertise. The skill chooses quick, managed, or package mode, selects one owner role, limits advisors to 0-2, governs execution through Brain/Hands/Review, and upgrades to A/B evaluation or audit when needed. Trigger when the user asks who should lead, who should collaborate, how to coordinate multiple roles, how to execute a task seriously end-to-end, or how to prove a candidate workflow is better than the incumbent.
---

# Partner Skill

> First decide how much governance this task deserves. Then decide who should lead it.

## Core Position

This is a governance skill.

It is responsible for:

1. task-mode classification
2. owner selection
3. advisor selection
4. output protocol control
5. escalation to stronger review or audit

It is not responsible for:

- becoming the domain expert
- replacing specialist judgment
- producing domain content just because it can

`Jobs`, `Kandle`, `Coding`, `Elon`, `Andy Grove`, `Goldratt`, and `Atul Gawande` own domain judgment.
`partner-skill` governs the workflow around them.

## First Responsibility: Task-Mode Classification

Before routing any role, classify the task into one of three modes:

- `quick`
- `managed`
- `package`

Read `references/task-mode-classification.md` when the mode is not obvious.

### quick

Use for low-complexity tasks with one owner, small process surface, and limited coordination cost.

Required output:

```markdown
Goal:
Action:
Risk:
Done:
```

### managed

Use for tasks that need one owner, up to two advisors, and explicit state tracking.

Required output:

```markdown
Owner:
Advisors:

Brain:
Action:
State:
Review:
```

### package

Use for long-running, high-investment, or failure-sensitive tasks.

Required output:

```markdown
Owner:
Advisors:

Brain:
Action:
State:
Review:
Round Status:
Verification:
Open Blockers:
Artifacts:
```

If the task is high-risk, add:

```markdown
Audit:
```

## Fixed State Slots

`State` is not free-form prose.
Use these slots:

- `Input`
- `Completed Actions`
- `Current Blocker`
- `Outputs`
- `Waiting On`
- `Residual Risks`

Templates live in `references/serious-execution-templates.md`.

## Audit Upgrade

For high-risk tasks, read `references/audit-protocol.md` and append `Audit`.

Audit must answer:

- what resources were read
- what objects were changed
- what permissions were used
- what actions were explicitly confirmed
- what actions are irreversible

## When To Use

Use this skill when:

- the user wants multi-role coordination
- the user asks who should lead or who should support
- the task spans product, research, implementation, operations, constraints, or reliability
- the task needs explicit governance strength rather than ad hoc collaboration
- the user asks for serious execution, full-package delivery, or multi-round review
- the user wants to evaluate whether a new workflow or skill is actually better than the incumbent

Do not use it for:

- simple one-off answers
- pure translation, rewriting, or summarization
- tasks where a single domain skill is explicitly requested and no coordination is needed

## Governance Flow

1. Classify task mode
2. Choose exactly one owner
3. Add 0-2 advisors if needed
4. Produce the owner judgment as `Brain`
5. If execution is needed, define a `Hands` contract
6. Produce `State` using fixed slots
7. Produce `Review`
8. If mode is `package`, also produce:
   - `Round Status`
   - `Verification`
   - `Open Blockers`
   - `Artifacts`
9. If risk is high, append `Audit`

## Role Routing

Detailed mapping lives in `references/role-routing-matrix.md`.

Keep the main discipline simple:

- one owner only
- advisors capped at 2
- advisors patch blind spots
- owner states what was accepted, rejected, and why

## Manager-Agent Layering

Read `references/manager-agent-protocol.md` when the task has:

- long execution chains
- noisy tool failures
- retries
- permission boundaries
- asynchronous progress
- explicit blocker management

Short version:

- `Brain` decides
- `Hands` executes
- `Review` verifies

## Serious Execution

`package` mode is the default home for serious execution.

Read:

- `references/serious-execution-protocol.md`
- `references/serious-execution-templates.md`

## A/B Evaluation

When the user asks whether a candidate is actually better than the incumbent, read:

- `references/ab-evaluation-protocol.md`

Use A/B mode to compare:

- current protocol vs revised protocol
- no-partner baseline vs partner-governed workflow
- incumbent vs candidate skill behavior

Do not claim improvement unless the candidate passes the gate.

## Reference Navigation

- `references/task-mode-classification.md`
  - decide governance strength before routing roles
- `references/manager-agent-protocol.md`
  - separate Brain, Hands, and Review
- `references/role-routing-matrix.md`
  - choose owner and advisors
- `references/conflict-resolution.md`
  - resolve vetoes and tie-breaks
- `references/serious-execution-protocol.md`
  - run package-mode tasks end-to-end
- `references/serious-execution-templates.md`
  - use fixed templates for State, Verification, and delivery
- `references/audit-protocol.md`
  - add audit information for high-risk tasks
- `references/ab-evaluation-protocol.md`
  - compare incumbent vs candidate and enforce gates
