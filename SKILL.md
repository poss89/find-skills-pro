---
name: find-skills-pro
description: >
  Discover, verify, security-scan, compare, and recommend agent skills when the
  user needs a reusable capability that may already exist. Use for skill
  discovery, provenance/current-source checks, NVIDIA SkillSpector review,
  behavioral/security review, overlap analysis, host/scope routing, and a clear
  INSTALL / SKIP / ON-DEMAND / REPLACE recommendation. It may install a specific
  skill only after explicit user approval for that exact candidate and action,
  then must perform post-install verification. Any persistent skill-state change
  requires explicit user approval for that exact candidate and action.
enabled: true
---

# Find Skills Pro

Find Skills Pro is a governed skill-discovery and installation workflow.

Its job is not merely to find popular skills. It must determine whether a
candidate is current, trustworthy enough to consider, useful relative to the
existing stack, appropriate for the target host/scope, and safe to install.

Security approval alone is never sufficient: provenance, quality, overlap,
routing, and scope still matter.

## Core Pipeline

Use this pipeline in order:

1. DISCOVERY
2. PROVENANCE / CURRENT SOURCE
3. NVIDIA SKILLSPECTOR
4. BEHAVIORAL / SECURITY REVIEW
5. OVERLAP REVIEW
6. HOST / SCOPE + ROUTING
7. RECOMMENDATION
8. USER APPROVAL
9. INSTALLATION
10. POST-INSTALL VERIFY

Do not skip directly from discovery to installation.

## When to Use

Use this skill when the user:

- asks to find a skill for a capability or workflow;
- asks whether a reusable skill already exists;
- wants to extend an agent with a specialist capability;
- asks for the best skill among several candidates;
- asks whether a discovered skill is worth installing;
- wants a candidate security-checked before installation;
- wants to install a skill after governed review.

Do not invoke this workflow merely because an ordinary task could theoretically
be packaged as a skill. Use it when skill discovery or stack extension is part
of the user's actual goal.

## Audited Skills CLI Pin

The currently audited CLI pin is `skills@1.7.0`.

Use the exact pinned version in command examples and execution:

```bash
npx skills@1.7.0 find react performance
```

Do not silently replace the pin with `latest`. Before changing the pin, verify
the current upstream package identity, release, provenance, and relevant
security behavior, then re-run the security gate on this skill if its commands
change.

Useful CLI operations include:

```bash
npx skills@1.7.0 find react performance
npx skills@1.7.0 add vercel-labs/agent-skills --skill react-best-practices
```

Installation commands shown to the user are proposals until the explicit
approval gate below is satisfied.

## Step 1 — Discovery

Understand the requested capability first:

- domain;
- concrete task;
- target host or agent if known;
- whether the capability should be reusable across projects or specific to one;
- whether an existing installed skill may already cover the role.

Search current sources rather than relying only on remembered candidates.
Useful discovery sources can include the Skills CLI, skills.sh, current upstream
repositories, and official publisher documentation.

Popularity and install count are discovery signals only. They are not security
or quality guarantees.

## Step 2 — Provenance / Current Source

For each serious candidate, establish:

- exact skill name;
- exact repository and skill path;
- author or organization;
- official vs third-party status;
- license when relevant;
- current upstream version, tag, or commit when available;
- whether the copy being reviewed is the same source intended for installation.

Prefer primary upstream sources.

Do not treat a registry summary, stale local copy, fork, mirror, or cached result
as equivalent to the current intended installation source without checking.

### Pre-Approval Read-Only Boundary

Until Step 8 is explicitly approved by the user, this workflow is limited to
non-persistent inspection activities: discovery, provenance checks, temporary
candidate retrieval for review, static scanning, comparison, analysis, and
recommendation.

Before approval, it must not change installed skill state, host configuration,
routing state, enablement state, or any other persistent skill configuration.

## Step 3 — NVIDIA SkillSpector

Before recommending `INSTALL` or `REPLACE`, send the exact candidate artifact
through NVIDIA SkillSpector when it is available.

Use the baseline static-only scan profile from the candidate's temporary
inspection directory:

```bash
skillspector scan . --no-llm
```

SkillSpector is the external security gate for the candidate. Its report is
returned to Find Skills Pro as security evidence.

- If the candidate passes the defined security gate, control returns to Find
  Skills Pro for behavioral/quality review, overlap analysis, host/scope
  routing, and recommendation.
- If the candidate fails the gate or has unresolved findings, do not proceed
  toward installation. Surface the findings and, when appropriate, propose a
  remediation or a different candidate.
- A security pass is not installation authorization.

Run the scan against the exact candidate artifact or exact candidate skill
directory, not an unrelated repository copy.

If the candidate is first retrieved for inspection, keep that retrieval
temporary and isolated from installed skill state. Do not execute candidate
scripts, hooks, installers, or arbitrary code merely to scan it.

Treat the report as security evidence, not as the sole product-quality decision:

- `0/100 SAFE` does not resolve overlap or quality concerns;
- findings must be reviewed and explained before the workflow continues;
- a justified false positive may be accepted if clearly explained;
- incomplete or partial inspection must be disclosed;
- deeper semantic analysis is optional unless the risk profile justifies it.

If the candidate cannot be inspected adequately, do not recommend it as ready
for installation.

### Scanner-Result Integrity

SkillSpector evidence must describe what actually ran against the exact candidate
artifact. Never predict or fabricate a scanner result.

If SkillSpector has not actually run:

- report `SkillSpector: NOT_RUN`, or `SkillSpector: UNAVAILABLE` when that is
  the reason;
- label any fallback inspection as `MANUAL STATIC REVIEW ONLY`;
- do not predict a score, severity, recommendation, or verdict such as
  "expected 0/100", "likely SAFE", or equivalent;
- do not call a manual review `PASS`, `SAFE`, `security-cleared`, or use
  wording that can be confused with a SkillSpector result;
- do not infer a scanner verdict merely because the artifact appears to contain
  only Markdown or other non-executable files.

Manual static review can surface risks, but it does not satisfy the external
SkillSpector gate.

If a candidate is otherwise strong enough to merit installation or replacement
but the required external gate has not run, describe it only as
`INSTALL — GATE PENDING` or `REPLACE — GATE PENDING`. It is not ready for
approval or installation. Stop before Step 8 until the exact artifact has a real
SkillSpector result or a verified external pre-install scan that satisfies the
same gate.

## Step 4 — Behavioral / Security Review

Inspect the candidate's actual instructions and bundled artifacts.

Check for, when applicable:

- shell commands and subprocess execution;
- package installation or mutable remote dependencies;
- network calls and remote downloads;
- hooks, scripts, binaries, or generated executables;
- credential, token, secret, cookie, environment, or private-file access;
- external uploads or data transmission;
- persistent writes or configuration changes;
- git, deployment, publishing, account, billing, or infrastructure actions;
- destructive or irreversible operations lacking explicit user approval;
- instructions that conflict with approval requirements or mandatory review requirements.

A skill can be useful and still require a Safety Gate.

## Step 5 — Overlap Review

Compare the candidate with the installed canonical stack before recommending a
new persistent copy.

Use these rules:

- light overlap / different roles -> KEEP BOTH;
- medium overlap / distinct value -> KEEP BOTH with clear boundaries;
- strong same-role overlap -> KEEP THE BETTER OPTION;
- if an excluded candidate contains a superior unique portion, preserve that
  portion only when provenance and license allow.

Prefer the narrowest relevant specialist for routine routing. Broad
orchestrators should not crowd out specialist skills.

Do not reinstall an existing capability under another name merely because it
appears popular.

## Step 6 — Host / Scope + Routing

Recommend the correct persistence scope rather than defaulting blindly.

General rule:

- reusable capability useful across projects -> user/private/global scope when
  the host supports it safely;
- project-specific product truth, repository conventions, or local workflow ->
  project scope;
- useful but specialist or infrequent capability -> ON-DEMAND may be better.

Host semantics differ. Never assume a CLI flag such as `-g` maps exactly to a
host's Private/User skill system. Verify the host-specific installation method.

Define a narrow description and trigger boundary so the new skill routes
naturally without creating avoidable collisions.

## Step 7 — Recommendation

Produce one clear outcome for each serious candidate:

- **INSTALL** — adds distinct value and passes the required gates;
- **SKIP** — insufficient value, quality, provenance, or safety;
- **ON-DEMAND** — useful, but not worth persistent installation;
- **REPLACE** — superior to an existing strong-overlap skill and worth a
  controlled migration.

For `INSTALL` or `REPLACE`, present at minimum:

- candidate and source;
- what it uniquely adds;
- freshness/provenance result;
- the actual SkillSpector result, or an explicit `NOT_RUN / UNAVAILABLE`
  status;
- material behavioral/security findings;
- overlap conclusion;
- recommended host/scope;
- routing boundary;
- exact proposed installation or replacement action.

When SkillSpector is required but still `NOT_RUN / UNAVAILABLE`, the
recommendation must carry `GATE PENDING` and must not be presented as safe,
cleared, approval-ready, or installation-ready.

## Step 8 — Mandatory Human Approval Gate

This is a hard boundary.

Before any installation, update, replacement, deletion, enable/disable action,
or other persistent mutation, present the recommendation and **STOP AND WAIT**.

Do not request Step 8 installation/replacement approval while a mandatory
SkillSpector gate is still `NOT_RUN / UNAVAILABLE`. Resolve or externally
satisfy that gate first.

Proceed only after explicit user approval for the specific candidate and the
specific proposed action.

Valid approval can be a direct instruction such as:

- "install this skill";
- "install Find X privately";
- "replace the old X with this one";
- an unambiguous "go" or equivalent when exactly one pending action has just
  been presented.

The following never count as installation approval by themselves:

- discovery;
- a high ranking or install count;
- `0/100 SAFE`;
- the agent's own recommendation;
- the user's general interest in the skill;
- approval previously given for another skill or another action.

If more than one materially different persistent action is pending, make the
approval scope explicit before executing them.

## Step 9 — Installation

After the approval gate is satisfied, execute only the approved action.

Rules:

- use the verified candidate/source;
- use the audited pinned CLI when the Skills CLI is the chosen mechanism;
- install only to the approved host/scope;
- do not add unrelated skills from the same repository;
- do not use overwrite, force, non-interactive, global, or broad wildcard flags
  merely for convenience;
- use such flags only when they are actually required for the approved target
  and their effect is understood;
- do not update, delete, replace, enable, or disable other skills unless that was
  explicitly part of the approved action;
- if the target host requires a UI upload or another host-specific mechanism
  that cannot be completed programmatically, prepare the correct artifact or
  exact steps and say that installation is not yet complete.

For `REPLACE`, preserve a recoverable backup of the existing skill when
practical before removing or overwriting it.

## Step 10 — Post-Install Verification

Do not declare success merely because an installer exited successfully.

Verify the resulting state using targeted checks appropriate to the host:

1. confirm the intended skill exists in the intended scope;
2. confirm no unexpected sibling skills were added;
3. confirm the installed identity/source is the approved one;
4. inspect the installed `SKILL.md` and relevant bundled files;
5. re-run the static SkillSpector gate on the installed copy when practical;
6. confirm routing/name collisions were not introduced;
7. report any difference between the approved plan and actual result.

If verification fails, do not silently repair or replace additional components.
Explain the discrepancy and request approval for any new persistent action.

## Special Rule for Newer Upstream Releases

A newer upstream release is a review signal only. It does not authorize any
persistent version change.

For an important changed skill:

1. inspect the current upstream;
2. compare it with the installed canonical copy;
3. review security and behavioral changes;
4. assess overlap/routing impact;
5. recommend the proposed version change;
6. obtain explicit user approval for that specific change;
7. apply only the approved change;
8. verify the resulting installed copy.

Find Skills Pro treats its own `SKILL.md`, package contents, configuration, and
runtime policy as read-only during normal execution. Changing Find Skills Pro
itself is outside this workflow and requires a separate explicit user request.

## When No Suitable Skill Exists

If no candidate survives the review:

- say so clearly;
- offer to perform the task with existing capabilities when appropriate;
- optionally suggest creating a custom skill if the workflow is genuinely
  reusable.

Creating a new persistent skill is itself a separate write action and requires
user approval before files are created or installed.

## Final Operating Principle

Before user approval, Find Skills Pro is limited to **discovering, reading,
comparing, scanning, analyzing, and recommending** through non-persistent
inspection methods.

Only after explicit user approval for the exact proposed action may the
workflow perform that specific persistent installation or state change.

SkillSpector supplies the candidate's security assessment; Find Skills Pro then
continues the remaining review and recommendation steps. Neither a security
pass nor Find Skills Pro's recommendation replaces explicit user control.
