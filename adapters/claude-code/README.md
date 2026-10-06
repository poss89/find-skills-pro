# Claude Code Adapter

**Status: adapter drafted — runtime validation pending**

Claude Code supports filesystem-based custom Skills.

## Recommended scope

Find Skills Pro is cross-project, so prefer personal scope:

```text
~/.claude/skills/find-skills-pro/SKILL.md
```

Project-only alternative:

```text
.claude/skills/find-skills-pro/SKILL.md
```

## Security gate

Claude Code's local shell/filesystem model is a strong fit for the full workflow:

```text
candidate → temporary inspection area → NVIDIA SkillSpector → return report
→ overlap/quality/scope review → user approval → install → verify
```

Do not install the candidate before the security and approval gates complete.

Official reference:
- https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
