# Partner Skill

`partner-skill` is a public Codex skill repository for orchestrating multi-role AI work with a manager-agent pattern.

The repository is designed around one primary entrypoint:

- `partner-skill` is the required top-level coordinator.

It can also bundle optional role skills in the same repository so users do not need to manage multiple repos if they prefer a single install surface.

## What This Repository Implements

This repository does **not** treat role coordination as “many personas talking at once”.
It implements a layered protocol:

- `Brain`: one owner role makes the primary judgment and defines the goal, success criteria, and tradeoffs.
- `Hands`: execution is expressed through contracts, not through raw tool noise leaking into planning.
- `Review`: verification, blocker reporting, residual risk, and A/B evaluation gates.

This means `partner-skill` is closer to a manager-agent protocol than a prompt wrapper.

## Core Design

The main skill enforces:

- exactly one owner role
- 0-2 advisor roles
- bounded advisor outputs
- `Brain / Action / Review` output structure
- serious execution mode for larger tasks
- A/B evaluation mode for skill iteration or candidate-vs-incumbent comparison

The repository also includes:

- routing rules
- role conflict rules
- serious execution templates
- manager-agent protocol references
- A/B evaluation protocol references

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
│   ├── manager-agent-protocol.md
│   ├── role-routing-matrix.md
│   ├── conflict-resolution.md
│   ├── serious-execution-protocol.md
│   ├── serious-execution-templates.md
│   └── ab-evaluation-protocol.md
└── skills/
    ├── steve-jobs-skill/
    ├── andy-grove-perspective/
    ├── goldratt-perspective/
    └── atul-gawande-perspective/
```

## Bundled Optional Skills

This repository currently bundles the following optional role skills:

- `steve-jobs-skill`
- `andy-grove-perspective`
- `goldratt-perspective`
- `atul-gawande-perspective`

These are optional. A user can install only `partner-skill`, or install `partner-skill` plus any subset of the bundled role skills.

At the moment, roles such as `Kandle`, `Coding`, and `Elon` are referenced by the protocol but are **not** bundled as standalone installable skills in this repository.

## Recommended Installation Modes

### Mode 1: Minimal Setup

Install only the top-level coordinator:

```powershell
python "C:\Users\10121\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" --repo Lucky-love-wxy/partner-skill --path partner-skill
```

Use this mode if:

- you only want the orchestration protocol
- you already have your own role skills
- you want a lightweight install

### Mode 2: Bundled Setup

Install the coordinator plus the bundled role skills:

```powershell
python "C:\Users\10121\.codex\skills\.system\skill-installer\scripts\install-skill-from-github.py" --repo Lucky-love-wxy/partner-skill --path partner-skill skills/steve-jobs-skill skills/andy-grove-perspective skills/goldratt-perspective skills/atul-gawande-perspective
```

Use this mode if:

- you want a single public repo as the installation surface
- you want `partner-skill` and role skills to stay version-aligned
- you do not want to manage multiple repositories

## How Users Should Configure It

The intended default is simple:

1. Install `partner-skill`
2. Optionally install bundled role skills
3. Let `partner-skill` act as the manager layer
4. Use role skills only when the manager decides they are needed

In practice:

- the user can configure only `partner-skill`
- the repository documentation tells them which bundled role skills are available
- advanced users can choose to install only the roles they want

## Dictionary / Prompt Library Integration

If your team maintains a private dictionary, style lexicon, prompt library, or internal phrasebook, the recommended approach is:

1. keep `partner-skill` public and generic
2. keep proprietary vocabulary or internal lexicons outside the public repo
3. document the integration point instead of hard-coding private data into `SKILL.md`

Recommended options:

- add a local private reference file after installation
- maintain an internal overlay repo
- keep internal vocabulary in a separate private skill and let `partner-skill` coordinate it

Do **not** publish proprietary dictionaries directly into this public repository unless you explicitly want them public.

## Current Manager-Agent Behavior

The current implementation supports:

- owner/advisor routing
- manager-agent framing
- Brain/Hands/Review separation
- serious execution mode
- A/B evaluation mode
- explicit conflict resolution and veto rules

The current A/B protocol evaluates:

- owner correctness
- advisor discipline
- output structure
- Hands contract quality
- review completeness
- serious-mode escalation
- hard failures such as multiple owners or missing review structure

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

This makes the public install path simpler than maintaining a network of separate submodule repositories.

If your local Codex environment provides a higher-level `skills add` wrapper, you can use that wrapper as an equivalent front-end. The canonical installation examples in this README use the installer helper because it explicitly supports multi-path installs from a single repository.

## License

MIT
