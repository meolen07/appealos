# AppealOS: Multi-Agent Denial Reversal System

**AppealOS** is a multi-agent A2A healthcare workflow concept for preparing clinician-reviewed appeal packets after a prior authorization or claim denial.

This project is built for the **Agents Assemble healthcare AI hackathon** using the **Prompt Opinion** platform.

> Uses synthetic data only. Not for clinical use.

---

## What it does

AppealOS helps a care team turn a denial case into a structured appeal workspace.

Given:

- a denial letter
- a requested service
- synthetic patient context
- payer policy criteria

AppealOS produces:

- denial reason summary
- payer criteria summary
- patient evidence timeline
- Evidence-to-Criteria Matrix
- missing documentation checklist
- Appeal Readiness Score
- draft appeal letter
- peer-to-peer call brief
- patient-friendly explanation
- safety and audit notes

The system is designed as a **multi-agent A2A workflow**, not a standalone chatbot.

---

## Why this matters

Prior authorization denials often require care teams to manually review denial letters, clinical notes, therapy history, medication history, exam findings, and payer criteria.

AppealOS focuses on the post-denial workflow:

1. Understand why the request was denied.
2. Find supporting evidence in the patient context.
3. Map payer criteria to available evidence.
4. Identify missing documentation.
5. Generate appeal materials for clinician review.

---

## Technical path

This project follows:

**Path B: A2A Agent**

The MVP is configured directly in the Prompt Opinion platform and published to the Prompt Opinion Marketplace.

No custom MCP server is required for the MVP.

---

## Multi-agent design

AppealOS is organized around one orchestrator and five specialist agents.

```text
AppealOS Orchestrator Agent
- Denial Interpreter Agent
- Clinical Evidence Finder Agent
- Policy Match Agent
- Appeal Packet Writer Agent
- Safety & Compliance Agent
```

### AppealOS Orchestrator Agent

Coordinates the workflow and produces the final appeal workspace.

### Denial Interpreter Agent

Extracts the denial reason, missing criteria, requested documents, and denial category from the denial letter.

### Clinical Evidence Finder Agent

Finds relevant evidence in synthetic patient context, such as therapies, medication trials, symptoms, exam findings, and encounters.

### Policy Match Agent

Compares payer criteria against patient evidence and creates the Evidence-to-Criteria Matrix.

### Appeal Packet Writer Agent

Drafts appeal materials, including the appeal letter, peer-to-peer brief, document checklist, and patient-friendly explanation.

### Safety & Compliance Agent

Checks for unsupported claims, fabricated evidence, PHI risk, diagnosis language, prescribing language, and missing clinician-review disclaimers.

---

## Demo case

The demo uses a synthetic lumbar spine MRI denial.

### Denial reason

The payer denied the MRI because the submitted documentation did not show:

- at least six weeks of conservative therapy
- qualifying neurologic findings
- red-flag symptoms

### Synthetic patient context

The synthetic patient record includes:

- chronic low back pain with right-sided radicular symptoms
- NSAID trial completed
- physical therapy completed for 8 weeks
- symptoms persisted despite conservative therapy
- positive straight-leg raise documented on follow-up

---

## Example input

```json
{
  "patient_id": "synthetic-patient-001",
  "requested_service": "Lumbar spine MRI",
  "payer_name": "Synthetic Health Plan",
  "denial_letter_text": "Coverage denied because submitted documentation does not show at least six weeks of conservative therapy or qualifying neurologic findings.",
  "payer_policy_text": "Lumbar spine MRI may be considered for review when symptoms persist despite conservative therapy, conservative therapy has been attempted for approximately six weeks, or relevant neurologic findings are documented.",
  "patient_context": {
    "condition": "Chronic low back pain with right-sided radicular symptoms",
    "therapy": "Physical therapy completed for 8 weeks",
    "medication_trial": "Ibuprofen trial completed",
    "follow_up": "Persistent right-sided radicular pain despite therapy and NSAID trial",
    "exam_finding": "Positive straight-leg raise documented on 2026-03-15"
  }
}
```

---

## Example output

### Evidence-to-Criteria Matrix

| Payer Criterion | Evidence Found | Source | Gap | Next Action |
|---|---|---|---|---|
| Six weeks conservative therapy | Physical therapy completed for 8 weeks | Synthetic therapy record | PT visit notes not attached | Attach PT records |
| Persistent symptoms | Persistent right-sided radicular pain | Follow-up note | Pain/function score missing | Add functional impact if available |
| Neurologic finding | Positive straight-leg raise documented | 2026-03-15 encounter | Clinician should verify wording | Attach encounter note |
| Medication trial | Ibuprofen trial completed | Synthetic medication history | Dose/dates not detailed | Attach medication history if available |

### Appeal Readiness Score

```text
82/100 - Medium-High readiness
```

This score estimates documentation completeness only. It does not determine medical necessity or guarantee payer approval.

---

## Safety boundaries

AppealOS is a workflow-support prototype.

It does **not**:

- diagnose
- prescribe
- determine medical necessity
- guarantee payer approval
- submit appeals automatically
- replace clinician judgment
- use real Protected Health Information

All generated materials require review by qualified healthcare professionals before use.

---

## Repository structure

```text
appealos/
├── README.md
├── LICENSE
├── .gitignore
├── marketplace-description.md
├── demo-script.md
├── agent-configuration/
│   ├── orchestrator-system-prompt.md
│   ├── denial-interpreter-agent.md
│   ├── clinical-evidence-finder-agent.md
│   ├── policy-match-agent.md
│   ├── appeal-packet-writer-agent.md
│   └── safety-compliance-agent.md
├── synthetic-data/
│   ├── synthetic-patient-001.json
│   ├── denial-letter-lumbar-mri.txt
│   └── payer-policy-lumbar-mri.md
├── docs/
│   ├── architecture.md
│   ├── safety-privacy.md
│   └── limitations.md
└── assets/
    ├── appealos-logo.png
    └── appealos-poster.png
```text
---
## Prompt Opinion Marketplace

Marketplace title:

```text
AppealOS: Multi-Agent Denial Reversal System
```

Short description:

```text
A multi-agent A2A healthcare workflow that turns denied prior authorizations into evidence-backed appeal packets for clinician review.
```

---

## Roadmap

Possible next steps:

- add more denial categories
- connect to a synthetic FHIR server
- support payer policy retrieval
- export appeal packets as documents
- add evidence confidence labels
- support production-grade A2A routing
- add evaluation cases for multiple payer denial patterns

---

## Disclaimer

This project is a hackathon prototype using synthetic or de-identified data only.

It is not a medical device.  
It does not provide medical advice.  
It does not diagnose or prescribe.  
It does not determine medical necessity.  
It does not guarantee payer approval.  
It is not intended for clinical use.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
