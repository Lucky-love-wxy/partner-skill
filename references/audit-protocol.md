# Audit Protocol

## Purpose

Audit is a visibility upgrade for high-risk tasks.
Use it when the task touches:

- public release
- irreversible actions
- elevated permissions
- sensitive resources
- high-stakes correctness

## Audit Questions

Audit should answer:

1. What resources were read?
2. What objects were changed?
3. What permissions were used?
4. Which actions were explicitly confirmed?
5. Which actions are irreversible?

## Output Format

```markdown
Audit:
- Resources Read:
- Objects Changed:
- Permissions Used:
- Confirmed Actions:
- Irreversible Actions:
```

## Rules

- Do not use Audit for every task.
- Do use Audit when the cost of hidden actions is high.
- Audit supplements Review; it does not replace Review.
- If no irreversible actions occurred, say `none`.
