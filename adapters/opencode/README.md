# OpenCode Adapter

**Status: adapter drafted — runtime validation pending**

OpenCode natively supports Agent Skills and loads them on demand.

## Recommended global scope

```text
~/.config/opencode/skills/find-skills-pro/SKILL.md
```

OpenCode also discovers global Agent-compatible skills under:

```text
~/.agents/skills/find-skills-pro/SKILL.md
```

Project scope is available under `.opencode/skills/`, `.claude/skills/`, or `.agents/skills/`.

## Permissions

OpenCode supports skill permission rules such as `allow`, `deny`, and `ask`. These host permissions are **additional** controls; they do not replace Find Skills Pro's explicit approval gate for persistent skill-state changes.

## Validation target

Prefer a single global copy and verify precedence so a project-local duplicate cannot silently override the canonical copy.

Official reference:
- https://opencode.ai/docs/skills
