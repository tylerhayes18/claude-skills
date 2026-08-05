# Claude Skills

Skills for [Claude Code](https://docs.claude.com/en/docs/claude-code), one directory per skill.

## Install

Copy a skill's directory into your personal skills folder, then restart Claude Code.

```bash
# macOS / Linux
cp -r SKILL_NAME ~/.claude/skills/
```

```powershell
# Windows
Copy-Item -Recurse SKILL_NAME "$env:USERPROFILE\.claude\skills\"
```

## Skills

| Skill | What it does |
| --- | --- |
| [insanely-great](insanely-great/SKILL.md) | Build to a higher bar than "working" using Steve Jobs' actual method, translated into engineering moves — design the call site before the implementation, diverge before committing, then run a subtraction pass. |
| [keyword-align](keyword-align/SKILL.md) | Revise existing copy so it uses VOLO Health's target search terms, changing terminology only and leaving structure, meaning, length and voice untouched. Outputs the revised text followed by a table of every change and the target term... |
