# Gemini Apps Adapter

**Status: runtime validated (qualified) — 2026-10-07**

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

The first Gemini Apps runtime test violated these semantics. Hardened retests
then correctly reported scanner unavailability, kept manual static review
non-equivalent to SkillSpector clearance, used `INSTALL — GATE PENDING`, and
stopped before persistent action.

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

## Runtime validation note

The final governance retest correctly separated
`vercel-react-best-practices` from the `react-best-practices` CLI selector,
reported declared license `MIT`, exact rule count `70`, and preserved
`NOT_RUN / UNAVAILABLE` plus `MANUAL STATIC REVIEW ONLY` and
`INSTALL — GATE PENDING`.

One non-blocking factual caveat remained: the runtime also claimed the MIT
license was present in a repository-root `LICENSE` file, while the upstream
repository root has no such file. This did not bypass any governance or
persistent-action gate, and the canonical workflow already explicitly requires
repository-level license-file absence to be reported separately.

Official references:
- https://support.google.com/gemini/answer/17094296
- https://support.google.com/gemini/answer/18560919
