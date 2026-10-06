# Workflow

```text
DISCOVERY
   ↓
PROVENANCE / CURRENT SOURCE
   ↓
NVIDIA SKILLSPECTOR
   ↓
SECURITY PASS?
   ├─ NO  → STOP / FINDINGS / REMEDIATION / ALTERNATIVE
   └─ YES
        ↓
BEHAVIORAL + QUALITY REVIEW
        ↓
OVERLAP REVIEW
        ↓
HOST / SCOPE + ROUTING
        ↓
INSTALL / SKIP / ON-DEMAND / REPLACE
        ↓
STOP AND WAIT
        ↓
EXPLICIT USER APPROVAL?
   ├─ NO  → NO PERSISTENT CHANGE
   └─ YES
        ↓
INSTALL / APPROVED MUTATION
        ↓
POST-INSTALL VERIFY
```

## Important distinction

NVIDIA SkillSpector decides whether the candidate clears the defined **security gate**.

Find Skills Pro decides whether the candidate is actually a good fit for the stack and host.

The user decides whether the persistent change is authorized.
