# Finding Unknowns Skill

A Codex skill for surfacing blind spots, hidden assumptions, and unclear success criteria before, during, and after complex AI-assisted work.

## Install

After this repository is on GitHub, install the skill with Codex's GitHub installer:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py --repo <owner>/<repo> --path skills/finding-unknowns
```

Restart Codex after installing.

## Use

Ask Codex for help with ambiguous, unfamiliar, subjective, or long-horizon tasks, for example:

```text
Use finding-unknowns to do a blind-spot pass before we implement this feature.
```

The skill helps Codex produce concrete artifacts such as unknowns briefs, prototype sets, high-leverage interviews, implementation plans, implementation notes, and reviewer explainers.
