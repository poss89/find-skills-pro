# Replit Adapter

**Status: validated**

Use the repository root `SKILL.md` as a Replit **Private/User** skill for cross-project reuse.

Recommended flow:

1. upload/package the canonical `SKILL.md`;
2. keep the skill in Private/User scope;
3. avoid a duplicate Project copy unless a project-specific fork is intentionally required;
4. verify the installed copy and routing behavior;
5. use NVIDIA SkillSpector against exact candidate artifacts discovered by Find Skills Pro.

Do not treat stale filesystem folders as authoritative when the Replit UI reports a different active Private/User state.
