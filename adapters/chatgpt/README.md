# ChatGPT Adapter

**Status: runtime validated — 2026-10-06**

## Goal

Use the canonical Find Skills Pro workflow in ChatGPT when the account/workspace exposes Skills.

OpenAI documents creating/uploading Skills from the Skills UI and also supports skills-only plugins.

## Important runtime boundary

Do **not** assume that every ChatGPT surface can execute a local `skillspector` binary.

If NVIDIA SkillSpector is unavailable in the active execution environment, Find Skills Pro must report `SkillSpector: NOT_RUN / UNAVAILABLE`. Manual static review must not be called `PASS`, `SAFE`, or security clearance, and the runtime must not predict an expected scanner score. Require an external/pre-install scan or stop before an approval-ready `INSTALL / REPLACE`.

## Validation checklist

- upload/import accepted;
- skill appears installed;
- natural-language routing works;
- scanner availability is established;
- explicit approval precedes any persistent change;
- post-install verification is feasible on that surface.

Official references:
- https://help.openai.com/en/articles/20001066-skills-in-chatgpt
- https://developers.openai.com/plugins/build/skills
