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

Installation or any other persistent skill-state change requires explicit user approval for the exact candidate and exact action.

See [`docs/security-model.md`](docs/security-model.md).

## Current validation

The canonical `SKILL.md` was tested with:

- NVIDIA SkillSpector `v2.12.0`
- static profile: `--no-llm`
- result: `7/100`
- severity: `LOW`
- recommendation: `SAFE`
- coverage: `100%`
- executable scripts: `No`

One `EA2` finding remained and was reviewed as an acceptable false positive caused by provenance-verification wording. The skill still contains an explicit pre-approval read-only boundary and a mandatory human approval gate before any persistent change.

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
| Codex | Adapter drafted | Runtime validation pending |
| ChatGPT | Adapter drafted | Runtime validation pending; product availability can vary |
| Claude | Adapter drafted | ZIP/custom-skill flow; runtime validation pending |
| Claude Code | Adapter drafted | Personal/project filesystem skill flow |
| OpenCode | Adapter drafted | Native Agent Skills discovery; runtime validation pending |
| TRAE | Adapter drafted | User environment already uses local skills; final runtime validation pending |
| Antigravity | Adapter drafted | Global/project scopes documented; token budget still matters |
| Gemini | Adapter drafted | Gemini Apps skills are current; exact install/scan path still needs runtime validation |

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
