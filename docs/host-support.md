# Host Support

Find Skills Pro uses **one canonical root `SKILL.md`**. Host adapters document packaging, scope, and runtime differences; they should not fork the core governance logic unless the host format genuinely requires it.

## Status definitions

- **Validated** — end-to-end host workflow has been exercised to the documented validation level.
- **Runtime validated** — the skill was loaded/discovered, routed naturally, and respected the persistent-action boundary; this does not imply SkillSpector is available on that host.
- **Retest pending** — the host loaded the skill, but a governance/runtime acceptance condition failed and must be retested after a canonical fix.
- **Adapter drafted** — official host mechanics are documented, but the exact Find Skills Pro package still needs runtime validation in that host.

## Matrix

| Host | Status | Preferred scope / packaging | SkillSpector strategy |
|---|---|---|---|
| Replit | **Validated** | Private/User for cross-project reuse | Local CLI validated |
| Codex | **Runtime validated** | Global/user skill in tested desktop environment | Use local CLI only when actually available; otherwise report `NOT_RUN / UNAVAILABLE` |
| ChatGPT | **Runtime validated** | Uploaded Skill in tested account | Never infer scanner availability; require actual scan or verified external pre-scan before approval-ready install/replace |
| Claude | **Runtime validated** | Custom Skill ZIP via claude.ai | Manual static review is not a scanner pass; use actual SkillSpector or verified external pre-scan |
| Claude Code | Adapter drafted | `~/.claude/skills/` personal or `.claude/skills/` project | Local CLI |
| OpenCode | Adapter drafted | `~/.config/opencode/skills/` global or `.opencode/skills/` project; also reads `.claude/skills` and `.agents/skills` | Local CLI |
| TRAE | **Runtime validated** | Personal/local skill layer in tested IDE + Work environment | If scanner is unavailable, report `NOT_RUN / UNAVAILABLE`; never predict a result |
| Antigravity | **Runtime validated** | `~/.gemini/config/skills/` global in tested environment | If scanner is unavailable, manual review remains explicitly non-equivalent |
| Gemini Apps | **Retest pending** | Uploaded Gemini Skill | First runtime test fabricated/predicted clearance semantics; retest only after canonical hardening |

## Codex

OpenAI documents Agent Skills as `SKILL.md`-based reusable workflows and supports skills-only portable plugins. Public/plugin packaging uses a root `plugin.json` plus `skills/<skill-name>/SKILL.md`. Codex and ChatGPT can share portable plugin packages, but installation and syncing can differ by product surface.

For Find Skills Pro, keep the root `SKILL.md` canonical and generate any Codex/plugin package from it.

## ChatGPT

ChatGPT Skills can be created or uploaded from the Skills UI when the account/workspace exposes the feature. Skills may also be distributed inside a skills-only plugin.

The tested target account accepted the uploaded skill and natural-language routing worked. Scanner availability still must be established per run; runtime validation does not authorize fabricated or predicted scanner results.

## Claude

`claude.ai` supports custom Skills uploaded as ZIP files through Settings > Features when the feature is available and code execution is enabled.

The tested Claude web/app accepted the packaged canonical `SKILL.md` and routed it correctly. In the runtime test, SkillSpector was unavailable and was correctly reported as not run; manual static review remained explicitly separate.

## Claude Code

Claude Code discovers custom skills from:

- personal: `~/.claude/skills/<skill-name>/SKILL.md`
- project: `.claude/skills/<skill-name>/SKILL.md`

Find Skills Pro is a general capability, so personal scope is the default recommendation.

## OpenCode

OpenCode natively discovers Agent Skills from several locations, including:

- global: `~/.config/opencode/skills/<name>/SKILL.md`
- project: `.opencode/skills/<name>/SKILL.md`
- Claude-compatible `.claude/skills/`
- Agent-compatible `.agents/skills/`

OpenCode supports per-skill permissions (`allow`, `deny`, `ask`). Find Skills Pro should keep its own human-approval gate regardless of host permission settings.

## TRAE

The target environment already uses personal/local Skills and shares local skill behavior across TRAE Code / Work in the current stack.

Find Skills Pro was installed and runtime-tested in both TRAE IDE and TRAE Work. Both respected the stop-before-persistent-action boundary. The IDE test used overly optimistic predicted scanner wording; the Unreleased canonical hardening explicitly forbids that wording.

## Antigravity

Current Google guidance documents:

- global: `~/.gemini/config/skills/`
- project/workspace: `<project-root>/.agents/skills/`

Find Skills Pro is generic, so global scope is preferred when the token budget permits it. The global skill was discovered and routed in Antigravity Agent Manager. Its runtime test also exposed overly strong manual-review wording, now forbidden by the Unreleased canonical hardening. Antigravity's token budget remains a host-specific constraint.

## Gemini Apps

Gemini Apps now supports reusable Skills for personal Google Accounts, with automatic relevance-based use and explicit invocation.

The Gemini Apps product is not the same runtime as Antigravity. Do not assume filesystem or local CLI capabilities. The first uploaded-skill runtime test failed governance acceptance because it predicted a SkillSpector score, called the candidate security-cleared without a real scan, and issued an approval-oriented INSTALL verdict. Gemini remains retest-pending until the hardened canonical skill is uploaded and passes the same runtime test.

## Validation rule

An adapter is promoted to **Validated** only after checking:

1. the skill is discoverable in the target host;
2. natural-language routing triggers appropriately;
3. the candidate security gate behaves as documented;
4. explicit approval is required before persistent changes;
5. post-install verification works;
6. duplicate identity / precedence behavior is understood.
