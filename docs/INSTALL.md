# Installing Maestro for Cursor

## Requirements

- [Cursor](https://cursor.com) with Agent Skills enabled
- Git (to clone the repository)

## Install steps

### macOS / Linux

```bash
git clone https://github.com/YOUR_ORG/maestro.git
mkdir -p ~/.cursor/skills
cp -r maestro ~/.cursor/skills/maestro
```

### Windows (PowerShell)

```powershell
git clone https://github.com/YOUR_ORG/maestro.git
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.cursor\skills"
Copy-Item -Recurse -Force maestro "$env:USERPROFILE\.cursor\skills\maestro"
```

### Verify layout

You should have:

```text
~/.cursor/skills/maestro/
├── SKILL.md
├── phases.md
├── examples.md
└── README.md
```

## Invoke Maestro

1. Open a new **Agent** chat in Cursor.
2. Type `/maestro` or attach the skill from the skill picker.
3. Prompt example:

   ```text
   /maestro full audit on src/api/ and firestore.rules
   ```

## Modes

| Prompt hint | Mode | Phases |
|-------------|------|--------|
| `full audit` | Full | All applicable phases |
| `quick audit` or `AUDIT_MODE: quick` | Quick | 0, 0.5, 1, 2, 5, 9 |
| `incident:` or `TRACK: incident` | Incident | 0.5 full, then targeted phases |

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Skill not in picker | Confirm folder name is `maestro` and `SKILL.md` exists; restart Cursor |
| Agent skips phases | Say explicitly: "Run all Maestro phases in order per SKILL.md" |
| Wrong skill loads | Use `/maestro` not generic "audit" without the skill attached |
| Updates | `cd maestro && git pull` then re-copy to `~/.cursor/skills/maestro` |

## Project-scoped install (team)

Copy into a repo instead of home:

```text
your-repo/.cursor/skills/maestro/
```

Commit `.cursor/skills/maestro/` so teammates get the same pipeline.
