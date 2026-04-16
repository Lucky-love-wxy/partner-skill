# Partner Skill

`partner-skill` is a public Codex skill repository for governing multi-role AI work through task-mode classification and a manager-agent pattern.

The first decision is not which role should speak.
The first decision is how much governance strength the task deserves.

## What This Repository Implements

This repository does **not** treat coordination as many personas talking at once.
It implements a layered governance protocol:

- `Mode`: classify the task as `quick`, `managed`, or `package`
- `Brain`: one owner role makes the primary judgment
- `Hands`: execution runs through explicit contracts
- `Review`: verification, blockers, residual risk, and A/B acceptance

This makes `partner-skill` a governance entrypoint, not a general-purpose domain expert.

## Core Design

The main skill enforces:

- task-mode classification before skill routing
- exactly one owner role
- 0-2 advisor roles
- bounded advisor outputs
- fixed output protocols by mode
- fixed `State` slots for managed and package tasks
- `Audit` escalation for high-risk tasks
- A/B evaluation gates for candidate-vs-incumbent comparison

The repository also includes:

- task-mode classification rules
- manager-agent protocol rules
- role conflict rules
- serious execution templates
- audit rules
- A/B evaluation rules

## Task Modes

### quick

Use for small tasks with one owner and minimal governance overhead.

Required output:

- `Goal`
- `Action`
- `Risk`
- `Done`

### managed

Use for tasks that need one owner, up to two advisors, and explicit state control.

Required output:

- `Brain`
- `Action`
- `State`
- `Review`

### package

Use for large, long-running, or high-investment tasks.

Required output:

- `Brain`
- `Action`
- `State`
- `Review`
- `Round Status`
- `Verification`
- `Open Blockers`
- `Artifacts`

For high-risk package tasks, add:

- `Audit`

## Fixed State Slots

In managed and package mode, `State` is not free-form prose.
It uses fixed slots:

- `Input`
- `Completed Actions`
- `Current Blocker`
- `Outputs`
- `Waiting On`
- `Residual Risks`

## Repository Layout

```text
partner-skill/
├── SKILL.md
├── README.md
├── LICENSE
├── .gitignore
├── .gitattributes
├── agents/
│   └── openai.yaml
├── references/
│   ├── task-mode-classification.md
│   ├── manager-agent-protocol.md
│   ├── role-routing-matrix.md
│   ├── conflict-resolution.md
│   ├── serious-execution-protocol.md
│   ├── serious-execution-templates.md
│   ├── audit-protocol.md
│   └── ab-evaluation-protocol.md
└── skills/
    ├── steve-jobs-skill/
    ├── andy-grove-perspective/
    ├── goldratt-perspective/
    └── atul-gawande-perspective/
```

## Bundled Optional Skills

This repository currently bundles these optional role skills:

- `steve-jobs-skill`
- `andy-grove-perspective`
- `goldratt-perspective`
- `atul-gawande-perspective`

They are optional.
Users can install only `partner-skill`, or install `partner-skill` plus any subset of the bundled role skills.

At the moment, roles such as `Kandle`, `Coding`, and `Elon` are referenced by the governance protocol but are not bundled as standalone installable skills in this repository.

## Recommended Installation Modes

### Mode 1: Minimal Setup

Install only the governance entrypoint:

```powershell
python "C:\Users\10121\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" --repo Lucky-love-wxy/partner-skill --path partner-skill
```

Use this mode if:

- you only want the governance protocol
- you already have your own role skills
- you want the lightest install

### Mode 2: Bundled Setup

Install the governance entrypoint plus bundled optional role skills:

```powershell
python "C:\Users\10121\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" --repo Lucky-love-wxy/partner-skill --path partner-skill skills/steve-jobs-skill skills/andy-grove-perspective skills/goldratt-perspective skills/atul-gawande-perspective
```

Use this mode if:

- you want one public repository as the install surface
- you want `partner-skill` and the bundled roles to stay version-aligned
- you do not want to manage multiple repositories

## How Users Should Configure It

The intended default is simple:

1. install `partner-skill`
2. optionally install bundled role skills
3. use `partner-skill` as the governance layer
4. let domain skills contribute only when the governance layer decides they are needed

In practice:

- a user can configure only `partner-skill`
- the repository documents which optional roles are bundled
- advanced users can install only the roles they want

## Dictionary / Prompt Library Integration

If your team maintains a private dictionary, style lexicon, prompt library, or internal phrasebook, the recommended approach is:

1. keep `partner-skill` public and generic
2. keep proprietary vocabulary outside the public repo
3. document the integration point instead of hard-coding private data into `SKILL.md`

Recommended options:

- add a local private reference file after installation
- maintain an internal overlay repo
- keep internal vocabulary in a separate private skill and let `partner-skill` coordinate it

Do **not** publish proprietary dictionaries directly into this public repository unless you explicitly want them public.

## Current V2 Behavior

The current implementation supports:

- task-mode classification
- owner/advisor routing
- manager-agent framing
- Brain/Hands/Review separation
- quick/managed/package governance
- audit upgrade for high-risk tasks
- A/B evaluation mode
- explicit conflict resolution and veto rules

The current A/B protocol evaluates:

- task-mode correctness
- owner correctness
- advisor discipline
- output structure
- Hands contract quality
- fixed State-slot discipline
- package-mode artifact and blocker discipline
- audit presence on high-risk tasks
- review completeness
- hard failures such as multiple owners, missing required blocks, or incorrect governance strength

## Validation

Validate the main skill locally with:

```powershell
python "C:\Users\10121\.codex\skills\.system\skill-creator\scripts\quick_validate.py" "D:\codex\project\partner-skill"
```

Expected output:

```text
Skill is valid!
```

## Publishing Notes

This repository is intentionally set up so that:

- `partner-skill` can stand alone
- bundled role skills can be installed from the same repo
- users do not need Git submodules
- documentation explains both minimal and bundled setup paths

This keeps the public installation path simpler than maintaining a network of separate repositories or submodules.

If your local Codex environment provides a higher-level `skills add` wrapper, you can use that wrapper as an equivalent front-end. The canonical examples in this README use the installer helper because it explicitly supports multi-path installs from a single repository.

## License

MIT
