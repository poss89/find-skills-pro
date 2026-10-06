# TRAE Adapter

**Status: runtime validated — TRAE IDE + TRAE Work, 2026-10-06**

The target stack already uses a personal/local skill layer across TRAE Code / Work.

## Porting rule

Use the canonical root `SKILL.md`; do not create a TRAE-specific rewrite unless runtime testing proves one is necessary.

## Validation target

Verify on the actual target installation:

- exact personal/global path;
- Code / Work visibility;
- enablement behavior;
- natural-language routing;
- local SkillSpector availability;
- post-install verification.

The tested IDE and Work runtimes both routed Find Skills Pro and stopped before persistent action. One IDE run predicted an expected SkillSpector result while the scanner was unavailable; the canonical workflow now forbids predicted scanner scores/verdicts and requires `NOT_RUN / UNAVAILABLE` instead.

Official product context:
- https://www.trae.ai/
- https://www.trae.ai/changelog
