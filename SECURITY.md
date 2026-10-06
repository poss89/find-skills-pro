# Security Policy

## Security philosophy

Find Skills Pro is designed around a mandatory human approval boundary.

Before explicit approval, the workflow should only perform non-persistent inspection: discovery, provenance checks, temporary candidate retrieval, scanning, comparison, analysis, and recommendation.

Persistent installation, replacement, update, deletion, enable/disable actions, or other skill-state changes require explicit approval for the exact candidate and exact action.

## Candidate scanning

When available, NVIDIA SkillSpector is used as an external security gate on the exact candidate artifact intended for installation.

A scanner pass does not authorize installation. It only allows the candidate to continue to quality, overlap, scope, routing, and recommendation review.

## Reporting a vulnerability

Please open a GitHub issue describing:

- affected version or commit;
- exact behavior;
- reproduction steps;
- why the behavior bypasses or weakens the approval/security model.

For sensitive disclosures, use the repository owner's preferred private GitHub security-reporting channel if enabled.

## Known scanner note

The 1.0.0 canonical `SKILL.md` produced a `7/100 LOW / SAFE` result under NVIDIA SkillSpector v2.12.0 with `--no-llm`.

One EA2 finding remained at the provenance-verification section and was manually reviewed as an acceptable false positive because the workflow explicitly forbids persistent changes before human approval.
