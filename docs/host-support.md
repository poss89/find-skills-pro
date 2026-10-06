# Host Support

Find Skills Pro uses one canonical core workflow, with host-specific packaging and installation rules.

## Status

### Replit — validated

Recommended scope: **Private/User** for cross-project reuse.

The canonical root `SKILL.md` has been validated in the Replit workflow.

### Codex / ChatGPT — planned

Target: Personal/global capability with the same governance model.

Status: adapter and runtime behavior still need host-specific validation.

### Claude — planned

Target: Claude-compatible Skill packaging.

Status: adapter and runtime behavior still need host-specific validation.

### TRAE — planned

Target: Personal/global/local skill compatible with TRAE Code / Work behavior.

Status: adapter and runtime behavior still need host-specific validation.

### Antigravity — planned

Target: lightweight persistent adapter where token budget permits.

Status: adapter and runtime behavior still need host-specific validation.

### Gemini — planned

Target: compatible standalone skill/port without assuming unsupported capabilities.

Status: adapter and runtime behavior still need host-specific validation.

## Rule

Do not copy host-specific installation commands across hosts blindly. A host adapter should only be marked validated after its actual persistence, routing, and post-install behavior have been verified.
