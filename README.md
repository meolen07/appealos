# AppealOS: Denial Reversal Agent

> Demo project for the Agents Assemble healthcare AI hackathon.  
> Uses synthetic or de-identified data only. Not for clinical use.

## Overview

AppealOS is an A2A-enabled healthcare workflow agent built for the Prompt Opinion multi-agent platform.

It helps healthcare teams respond to denied prior authorizations or denied claims by converting denial letters, synthetic FHIR-style patient context, and payer policy criteria into evidence-backed appeal packets for clinician review.

AppealOS does not replace clinicians, does not make autonomous coverage decisions, and does not submit appeals automatically. It prepares structured, auditable documentation that must be reviewed by qualified healthcare professionals.

## Problem

Prior authorization denials create delays, administrative burden, and fragmented follow-up work.

Care teams often need to manually review:

- denial letters
- clinical notes
- medication history
- prior therapies
- imaging history
- exam findings
- payer policy criteria
- missing documentation requirements

This work is time-consuming, repetitive, and difficult to coordinate across systems.

## Solution

AppealOS uses Generative AI and A2A collaboration to transform a denied authorization workflow into a structured appeal preparation workflow.

The agent can:

- summarize the denial reason
- identify payer-stated missing criteria
- analyze synthetic patient context
- find supporting clinical evidence
- identify missing documentation
- generate an appeal strategy
- draft an appeal letter
- create a peer-to-peer call brief
- create a patient-friendly explanation
- produce a safety and audit log

## Technical Path

This project follows:

**Path B: A2A Agent**

The agent is configured directly inside the Prompt Opinion platform and published to the Prompt Opinion Marketplace.

## How It Works

AppealOS receives healthcare workflow context such as:

```json
{
  "patient_id": "synthetic-patient-001",
  "fhir_base_url": "https://synthetic-fhir-server.example/r4",
  "fhir_access_token": "scoped_demo_token",
  "encounter_id": "synthetic-encounter-001",
  "requested_service": "Lumbar spine MRI",
  "payer_name": "Synthetic Health Plan",
  "denial_letter_text": "Coverage denied because submitted documentation does not show at least six weeks of conservative therapy or qualifying neurologic findings.",
  "payer_policy_text": "Lumbar spine MRI may be considered medically necessary when symptoms persist despite conservative therapy, or when neurologic deficits or red-flag symptoms are documented."
}