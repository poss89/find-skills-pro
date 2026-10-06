# Claude Adapter

**Status: adapter drafted — runtime validation pending**

## Packaging

Anthropic documents custom Skills on claude.ai as ZIP uploads through Settings > Features.

Package the canonical root `SKILL.md` as the skill payload. Do not fork the governance logic.

## SkillSpector boundary

Claude Skills have a code-execution environment, but Find Skills Pro must first verify that NVIDIA SkillSpector is actually available or can be used safely in that environment. If not, require an external pre-scan rather than fabricating a security pass.

## Scope

Custom claude.ai Skills are user-specific; they are separate from Claude Code filesystem Skills and from API/workspace Skills.

Official reference:
- https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
