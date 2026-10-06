# Changelog

All notable changes to Find Skills Pro will be documented here.

## 1.0.0 — 2026-10-06

Initial public release.

### Added

- governed skill discovery workflow;
- provenance/current-source verification;
- NVIDIA SkillSpector candidate security gate;
- behavioral/security review;
- overlap analysis;
- host/scope and routing recommendations;
- `INSTALL / SKIP / ON-DEMAND / REPLACE` outcomes;
- mandatory explicit human approval before persistent changes;
- post-install verification;
- pinned Skills CLI policy (`skills@1.7.0`);
- Replit validation and host-porting roadmap.

### Security validation

Canonical `SKILL.md` tested with NVIDIA SkillSpector v2.12.0 using `--no-llm`:

- score: 7/100;
- severity: LOW;
- recommendation: SAFE;
- coverage: 100%;
- executable scripts: none;
- one EA2 finding reviewed as an acceptable false positive.
