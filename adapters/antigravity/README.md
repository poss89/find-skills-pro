# Antigravity Adapter

**Status: runtime validated — Agent Manager, 2026-10-06**

Google documents two primary Skill scopes:

Global:

```text
~/.gemini/config/skills/find-skills-pro/SKILL.md
```

Project/workspace:

```text
<project-root>/.agents/skills/find-skills-pro/SKILL.md
```

Find Skills Pro is generic, so global scope is preferred when the host token budget permits it.

## Token-budget rule

Antigravity may exclude skills/tools when the resident context budget is exceeded. Keep this adapter lean and avoid bundling redundant documentation into the active skill package.

## Runtime boundary

The global skill was discovered and routed in Agent Manager. If SkillSpector is unavailable, Antigravity must report `NOT_RUN / UNAVAILABLE`; manual static review must not be labeled `PASS`, `SAFE`, or security-cleared and must not predict a scanner score.

Official reference:
- https://codelabs.developers.google.com/getting-started-with-antigravity-skills
