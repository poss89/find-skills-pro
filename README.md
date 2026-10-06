# Find Skills Pro

**Find Skills Pro** is a governed workflow for discovering, security-scanning, comparing, and installing agent skills without giving up human control.

It extends ordinary skill discovery with provenance checks, an external NVIDIA SkillSpector security gate, behavioral review, overlap analysis, host/scope routing, explicit user approval, and post-install verification.

> **Core principle:** a security pass is evidence, not permission to install.

## Why this exists

Typical skill discovery flows stop at “find something popular and install it.” Find Skills Pro adds a governance layer:

1. **DISCOVERY**
2. **PROVENANCE / CURRENT SOURCE**
3. **NVIDIA SKILLSPECTOR**
4. **BEHAVIORAL / SECURITY REVIEW**
5. **OVERLAP REVIEW**
6. **HOST / SCOPE + ROUTING**
7. **RECOMMENDATION**
8. **USER APPROVAL**
9. **INSTALLATION**
10. **POST-INSTALL VERIFY**

The workflow can recommend:

- `INSTALL`
- `SKIP`
- `ON-DEMAND`
- `REPLACE`

Before explicit approval, all work is limited to non-persistent inspection and analysis.

## Security model

Find Skills Pro treats NVIDIA SkillSpector as an external security gate for each candidate skill.

A candidate is discovered and materialized temporarily, scanned, and then returned to Find Skills Pro for the remaining quality, overlap, routing, and scope review.

A SkillSpector `SAFE` result **never** means “install automatically.”

If SkillSpector did not actually run, Find Skills Pro must say
`NOT_RUN / UNAVAILABLE`; manual static review must not be reported as
`PASS`, `SAFE`, or a predicted scanner score.

Installation or any other persistent skill-state change requires explicit user approval for the exact candidate and exact action.

See [`docs/security-model.md`](docs/security-model.md).

## Current validation

The v1.1.0 release-candidate canonical `SKILL.md` at commit
`9bfaa7f61eafa601b22ef5f484add71791292c81` was freshly tested with:

- NVIDIA SkillSpector `v2.12.0`
- static profile: `--no-llm`
- canonical SHA256: `ffbebdf563b5095596ff6f0142e8ce60d2c15b81c3d02a9e3943f6e5cadb3206`
- score: `7/100`
- severity: `LOW`
- recommendation: `CAUTION`
- coverage: `100%`
- executable scripts: `No`

One `EA2` finding remained and was manually accepted as a qualified false
positive: it is triggered by provenance/current-source verification wording,
while the canonical workflow separately enforces a pre-approval read-only
boundary and mandatory human approval before persistent changes.

SkillSpector also reported one `reference_missing` ledger exception caused by
path-like metadata/reference wording; no bundled artifact is actually missing.
With `--no-llm`, semantic analyzers are intentionally disabled. The inspected
artifact still reported 100% coverage, one fully inspected file, zero partially
or entirely uninspected files, and no executable scripts.

Scanner output can vary across SkillSpector versions.

## Skills CLI

The currently audited CLI pin in the canonical skill is:

```bash
npx skills@1.7.0
```

The pin is intentional. Do not silently replace it with `latest`; re-audit before changing it.

## Host support

| Host | Status | Notes |
|---|---|---|
| Replit | **Validated** | Private/User workflow tested |
| Codex | **Runtime validated** | Global skill discovered and routed; approval boundary respected |
| ChatGPT | **Runtime validated** | Uploaded skill routed correctly; scanner absence was not fabricated |
| Claude | **Runtime validated** | Uploaded ZIP routed correctly; manual review kept distinct from SkillSpector |
| Claude Code | Adapter drafted | Personal/project filesystem skill flow |
| OpenCode | Adapter drafted | Native Agent Skills discovery; runtime validation pending |
| TRAE | **Runtime validated** | IDE + Work routed correctly; scanner-result wording hardened in Unreleased |
| Antigravity | **Runtime validated** | Global skill routed in Agent Manager; scanner-result wording hardened in Unreleased |
| Gemini | **Runtime validated (qualified)** | Hardened retests respected scanner/provenance gates; one non-blocking repository-level license factual caveat remained |

See [`docs/host-support.md`](docs/host-support.md).

## Repository layout

```text
.
├── SKILL.md
├── README.md
├── LICENSE
├── THIRD_PARTY_NOTICES.md
├── CHANGELOG.md
├── SECURITY.md
├── docs/
│   ├── security-model.md
│   ├── workflow.md
│   └── host-support.md
└── adapters/
    ├── replit/
    ├── codex/
    ├── chatgpt/
    ├── claude/
    ├── claude-code/
    ├── opencode/
    ├── trae/
    ├── antigravity/
    └── gemini/
```

The root `SKILL.md` is the **single canonical skill definition**. Host adapters should reference or package that file rather than fork its logic unless a host genuinely requires a different format.

## Replit

For Replit, use the canonical root `SKILL.md` as a Private/User skill so it can be reused across projects.

See [`adapters/replit/README.md`](adapters/replit/README.md).

## Non-affiliation

Find Skills Pro is an independent project. It is not affiliated with or endorsed by NVIDIA or Vercel.

NVIDIA SkillSpector is used as an external security scanner. Portions of the original skill-discovery concept were adapted from Vercel's MIT-licensed `vercel-labs/skills` project; see [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md).

## License

MIT. See [`LICENSE`](LICENSE).
