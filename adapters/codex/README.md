# Codex Adapter

**Status: adapter drafted — runtime validation pending**

## Goal

Expose the canonical Find Skills Pro workflow to Codex without forking the root `SKILL.md`.

## Packaging

OpenAI supports Agent Skills and skills-only portable plugins. For a portable package, use:

```text
find-skills-pro/
├── plugin.json
└── skills/
    └── find-skills-pro/
        └── SKILL.md
```

Generate `skills/find-skills-pro/SKILL.md` from the repository root `SKILL.md`; do not maintain it independently.

## Runtime expectations

Where Codex has local shell/filesystem access, NVIDIA SkillSpector can remain the external candidate-security gate.

Persistent installation still requires the explicit user-approval gate in the canonical skill.

## Validation checklist

- install/package is discoverable;
- implicit routing works;
- exact candidate can be scanned;
- security pass returns control to Find Skills Pro;
- explicit approval precedes install;
- post-install verification succeeds.

Official references:
- https://developers.openai.com/plugins/build/skills
- https://developers.openai.com/plugins/build/plugins
