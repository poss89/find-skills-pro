# Antigravity Adapter

**Status: adapter drafted — runtime validation pending**

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

Official reference:
- https://codelabs.developers.google.com/getting-started-with-antigravity-skills
