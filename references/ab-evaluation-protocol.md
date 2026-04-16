# A/B Evaluation Protocol

## Goal

Prove whether the candidate is actually better than the incumbent.
Do not confuse documentation completeness with behavioral improvement.

## Comparison Objects

- `incumbent`: the current version, prior version, or no-partner baseline
- `candidate`: the revised protocol, revised skill behavior, or partner-governed version

Comparator logic should judge outputs, not the implementation diff.

## Target Vector

Do not collapse everything into one score too early.
Evaluate at least:

- mode classification correctness
- owner correctness
- advisor discipline
- Brain clarity
- Hands contract quality
- fixed State-slot discipline
- Review completeness
- package-mode output completeness
- Audit presence on high-risk tasks
- safety boundary non-regression
- output executability

## Test Set Layers

### Dev Set

Use for protocol shaping.
Do not use it as the final acceptance surface.

### Holdout Set

Keep answers hidden during revision.
Use it for final acceptance.

### Comparator Set

Use for A/B comparison between incumbent and candidate.

### Live Canary Set

Use only when real traffic or real usage examples are available and appropriate.

## Minimum Coverage

One evaluation cycle should cover at least:

1. a `quick` task
2. a `managed` task
3. a `package` task
4. a safety or reliability-sensitive task
5. a skill-evaluation task

## Per-Case Scoring

Use 0-2 scoring:

- `0`: missing key protocol behavior or worse than the baseline
- `1`: partially correct but with meaningful gaps
- `2`: mode, routing, execution discipline, and review quality are all acceptable

## Hard Failures

Record any of these as hard failures:

- mode classification is clearly wrong
- multiple owners speak as equals
- advisors exceed 2
- required output block is missing
- managed or package mode uses narrative State instead of fixed slots
- package mode omits `Round Status`, `Verification`, `Open Blockers`, or `Artifacts`
- high-risk work omits `Audit`
- execution claims success without visible validation
- raw execution noise leaks into planning output
- safety or permission boundaries regress

## Gate

The candidate only passes if:

- it wins at least 4 of 5 cases
- total score exceeds the incumbent
- there are no hard failures
- it wins at least one `quick`, one `managed`, and one `package` case
- its output is more executable, not merely longer

If the candidate is more verbose but not more governable, fail it.

## Comparator Output

```markdown
Incumbent:
Candidate:

Test Set:
- prompt count:
- coverage:

Win/Loss Table:
| Case | Winner | Reason | Hard Failure |
|---|---|---|---|

Gate Decision:
- pass/fail:
- why:
- required fix:
```

## Human Acceptance

Human review should answer:

- where the candidate won
- where it lost
- what it traded away
- whether the stronger governance is worth keeping
