# Gemini Apps Adapter

**Status: retest pending — first runtime acceptance failed scanner-result semantics**

Gemini Apps now supports reusable Skills on eligible personal Google Accounts. Skills can be automatically applied when relevant or explicitly invoked.

## Important distinction

Gemini Apps is **not** Antigravity. Do not copy Antigravity filesystem paths or assume local-shell capabilities.

## Security gate

Before claiming the full Find Skills Pro workflow on Gemini Apps, verify whether the active Skills runtime can execute NVIDIA SkillSpector or otherwise call a trusted external scan path.

If the scanner cannot run, the adapter must:

- report `SkillSpector: NOT_RUN / UNAVAILABLE`;
- label fallback inspection `MANUAL STATIC REVIEW ONLY`;
- never predict a score, severity, `SAFE`, or other scanner verdict;
- never call a manual review `PASS` or security clearance;
- never present `INSTALL / REPLACE` as approval-ready while the gate is pending.

The first Gemini Apps runtime test violated these semantics, so the adapter remains retest-pending until the hardened canonical skill passes a fresh test.

## Provenance and command integrity

Gemini must prefer exact primary-upstream metadata over registry, mirror, cached,
or secondary-source claims. It must not merge conflicting license, identity,
version, or capability-count claims. If primary upstream cannot resolve a
conflict, report `UNKNOWN / CONFLICTING`.

When upstream `SKILL.md` frontmatter contains `name:`, Gemini must report that
exact value as the canonical declared skill identity. Repository directory
names, registry aliases/slugs, package names, and CLI `--skill` selectors are
separate identifiers and must be labeled separately when they differ.

When the exact candidate `SKILL.md` explicitly declares `license:` or other
frontmatter metadata, report it as the candidate's declared metadata. A missing
repository-level `LICENSE` file is a separate repository fact and does not by
itself make the declared skill license `UNKNOWN / CONFLICTING`.

Use `UNKNOWN / CONFLICTING` only when primary-upstream evidence itself is
missing or contradictory. When primary upstream declares an exact rule or
capability count, report the exact value rather than an approximation such as
`70+`.

Do not present CLI flags or options unless they were verified for the exact
pinned tool/version.

Official references:
- https://support.google.com/gemini/answer/17094296
- https://support.google.com/gemini/answer/18560919
