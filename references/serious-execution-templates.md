# Serious Execution Templates

## Quick Template

```markdown
Goal:
- what must happen

Action:
- next step

Risk:
- main uncertainty or downside

Done:
- what is already finished
```

## Managed Template

```markdown
Owner:
Advisors:

Brain:
- goal:
- facts:
- assumptions:
- tradeoff:
- recommendation:

Action:
- next step:
- execution contract:
- validation:

State:
- Input:
- CompletedActions:
- CurrentBlocker:
- Outputs:
- WaitingOn:
- ResidualRisks:

Review:
- verified:
- blocker:
- residual risk:
- next action:
```

## Package Template

```markdown
Owner:
Advisors:

Brain:
- goal:
- success criteria:
- accepted reasoning:
- rejected reasoning:
- why:

Action:
- current package:
- execution contract:
- validation plan:

State:
- Input:
- CompletedActions:
- CurrentBlocker:
- Outputs:
- WaitingOn:
- ResidualRisks:

Review:
- findings:
- fixed:
- not fixed:
- residual risk:
- escalation:

Round Status:
- round:
- phase:
- complete:
- next:

Verification:
- build:
- test:
- lint:
- manual:
- evidence:

Open Blockers:
- blocker:
- owner:
- unblock condition:

Artifacts:
- files:
- reports:
- screenshots:
- notes:
```

State is mandatory for `managed` and `package`.
For package mode, update the same State block across rounds instead of rewriting free-form.

## Audit Template

```markdown
Audit:
- Resources Read:
- Objects Changed:
- Permissions Used:
- Confirmed Actions:
- Irreversible Actions:
- Trigger:
```
