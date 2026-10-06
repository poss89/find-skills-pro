# Host Support

Find Skills Pro uses **one canonical root `SKILL.md`**. Host adapters document packaging, scope, and runtime differences; they should not fork the core governance logic unless the host format genuinely requires it.

## Status definitions

- **Validated** — tested in the target host/runtime.
- **Adapter drafted** — official host mechanics are documented, but the exact Find Skills Pro package still needs runtime validation in that host.

## Matrix

| Host | Status | Preferred scope / packaging | SkillSpector strategy |
|---|---|---|---|
| Replit | **Validated** | Private/User for cross-project reuse | Local CLI validated |
| Codex | Adapter drafted | Agent Skill / skills-only plugin; user or repo scope depending install surface | Local/desktop CLI where available |
| ChatGPT | Adapter drafted | Upload/install Skill or skills-only plugin when Skills are available | Use only where execution environment can run the scanner; otherwise require external scan |
| Claude | Adapter drafted | Custom Skill ZIP via claude.ai Settings > Features | Require SkillSpector availability or external pre-scan |
| Claude Code | Adapter drafted | `~/.claude/skills/` personal or `.claude/skills/` project | Local CLI |
| OpenCode | Adapter drafted | `~/.config/opencode/skills/` global or `.opencode/skills/` project; also reads `.claude/skills` and `.agents/skills` | Local CLI |
| TRAE | Adapter drafted | Personal/local skill layer already used in the target environment | Local CLI if installed |
| Antigravity | Adapter drafted | `~/.gemini/config/skills/` global or `.agents/skills/` project | Local CLI; keep token budget in mind |
| Gemini Apps | Adapter drafted | Gemini Skills (personal account availability) | Do not claim local CLI scanning unless the execution surface actually supports it |

## Codex

OpenAI documents Agent Skills as `SKILL.md`-based reusable workflows and supports skills-only portable plugins. Public/plugin packaging uses a root `plugin.json` plus `skills/<skill-name>/SKILL.md`. Codex and ChatGPT can share portable plugin packages, but installation and syncing can differ by product surface.

For Find Skills Pro, keep the root `SKILL.md` canonical and generate any Codex/plugin package from it.

## ChatGPT

ChatGPT Skills can be created or uploaded from the Skills UI when the account/workspace exposes the feature. Skills may also be distributed inside a skills-only plugin.

Because availability and installation can vary by plan/workspace/product surface, do not mark this adapter validated until the exact target account is tested.

## Claude

`claude.ai` supports custom Skills uploaded as ZIP files through Settings > Features when the feature is available and code execution is enabled.

The Claude web/app adapter should package the canonical `SKILL.md` without changing its governance logic.

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

The public adapter remains marked unvalidated until Find Skills Pro itself is installed and tested there. Do not infer TRAE Work and TRAE Code behavior from another host.

## Antigravity

Current Google guidance documents:

- global: `~/.gemini/config/skills/`
- project/workspace: `<project-root>/.agents/skills/`

Find Skills Pro is generic, so global scope is preferred when the token budget permits it. Antigravity's token budget remains a host-specific constraint.

## Gemini Apps

Gemini Apps now supports reusable Skills for personal Google Accounts, with automatic relevance-based use and explicit invocation.

The Gemini Apps product is not the same runtime as Antigravity. Do not assume filesystem or local CLI capabilities. The adapter must be validated against the exact Gemini Skills creation/import surface before claiming full automated SkillSpector gating.

## Validation rule

An adapter is promoted to **Validated** only after checking:

1. the skill is discoverable in the target host;
2. natural-language routing triggers appropriately;
3. the candidate security gate behaves as documented;
4. explicit approval is required before persistent changes;
5. post-install verification works;
6. duplicate identity / precedence behavior is understood.
