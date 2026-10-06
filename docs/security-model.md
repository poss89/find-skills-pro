# Security Model

Find Skills Pro separates **security clearance**, **product/stack fit**, and **installation authorization**.

## 1. Candidate discovery

A candidate may be found through a registry, Skills CLI, `skills.sh`, upstream repositories, or publisher documentation.

Discovery signals such as popularity or install count are not treated as security evidence.

## 2. Provenance

Before scanning or recommending a candidate, establish the exact source intended for installation:

- repository;
- skill path;
- publisher;
- license where relevant;
- version/tag/commit when available;
- whether the reviewed artifact matches the intended install artifact.

## 3. External security gate

The exact candidate artifact is scanned with NVIDIA SkillSpector when available.

Baseline profile:

```bash
skillspector scan . --no-llm
```

If the candidate fails or contains unresolved findings, Find Skills Pro stops the installation path and surfaces the findings.

If the candidate passes, control returns to Find Skills Pro.

## 4. Remaining review

A security pass is not enough. Find Skills Pro still reviews:

- behavioral risk;
- quality;
- overlap with the canonical stack;
- host compatibility;
- correct persistence scope;
- routing boundaries.

## 5. Human approval

The workflow presents its recommendation and stops.

No persistent skill-state change occurs until the user explicitly approves the exact candidate and exact action.

## 6. Post-install verification

After approved installation, verify:

- intended skill exists;
- intended scope is correct;
- no unexpected siblings were added;
- installed source/identity matches approval;
- routing collisions were not introduced;
- scanner may be re-run on the installed copy.

A verification discrepancy is reported rather than silently repaired.
