# Changelog

All notable changes to Find Skills Pro will be documented here.

## 1.1.0 — 2026-10-07

### Changed

- split Codex and ChatGPT into separate host adapters;
- split Claude and Claude Code into separate host adapters;
- added an OpenCode adapter;
- refreshed the host-support matrix against current official host documentation;
- kept the root `SKILL.md` as the single canonical workflow source;
- hardened scanner-result semantics: no predicted SkillSpector scores/verdicts,
  no manual-review `PASS/SAFE` substitution, and explicit
  `NOT_RUN / UNAVAILABLE` states;
- blocked approval-ready `INSTALL/REPLACE` recommendations while a mandatory
  SkillSpector gate is pending;
- runtime-tested Codex, ChatGPT, Claude, TRAE IDE/Work, and Antigravity;
- hardened current-source provenance semantics for declared identity, license,
  version, exact capability counts, and pinned CLI command integrity;
- runtime-tested Gemini Apps after hardening; the final governance retest passed
  with one documented non-blocking repository-level license factual caveat.

### Security validation

Release-candidate canonical `SKILL.md` at commit
`9bfaa7f61eafa601b22ef5f484add71791292c81` tested with NVIDIA SkillSpector
v2.12.0 using `--no-llm`:

- SHA256: `ffbebdf563b5095596ff6f0142e8ce60d2c15b81c3d02a9e3943f6e5cadb3206`;
- score: 7/100;
- severity: LOW;
- recommendation: CAUTION;
- coverage: 100%;
- executable scripts: none;
- one EA2 finding manually accepted as a qualified false positive;
- one `reference_missing` ledger exception reviewed as non-material.

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
