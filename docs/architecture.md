# AppealOS Architecture

## Overview

AppealOS is a multi-agent A2A (Agent-to-Agent) healthcare workflow designed to transform denied prior authorizations into structured, evidence-backed appeal packets.

The system coordinates multiple specialized agents, each responsible for a specific task in the denial-to-appeal process.

---

## High-Level Flow

```text
Denial Letter
    ->
Denial Interpretation
    ->
Clinical Evidence Extraction
    ->
Policy Matching
    ->
Appeal Packet Generation
    ->
Safety and Compliance Review
    ->
Final Output for Clinician Review
```

---

## System Design

AppealOS follows a modular multi-agent architecture:

```text
AppealOS Orchestrator Agent
|- Denial Interpreter Agent
|- Clinical Evidence Finder Agent
|- Policy Match Agent
|- Appeal Packet Writer Agent
|- Safety and Compliance Agent
```

Each agent operates independently and produces structured outputs.

The Orchestrator coordinates the workflow and composes the final result.

---

## Agent Responsibilities

### 1. Orchestrator Agent

- Coordinates all agents
- Defines workflow sequence
- Combines outputs into a structured appeal packet
- Ensures output completeness and formatting

---

### 2. Denial Interpreter Agent

- Parses denial letters
- Extracts:
  - denial reason
  - requested service
  - missing criteria
  - appeal instructions

---

### 3. Clinical Evidence Finder Agent

- Extracts evidence from patient context
- Builds a patient timeline
- Identifies:
  - therapies
  - medications
  - symptoms
  - exam findings
- Flags missing documentation

---

### 4. Policy Match Agent

- Converts payer policy into structured criteria
- Maps evidence to each criterion
- Produces the Evidence-to-Criteria Matrix
- Identifies gaps and next actions

---

### 5. Appeal Packet Writer Agent

- Generates:
  - appeal strategy
  - draft appeal letter
  - peer-to-peer call brief
  - document checklist
  - patient-friendly explanation

---

### 6. Safety and Compliance Agent

- Validates output safety
- Detects:
  - PHI risks
  - unsupported claims
  - boundary violations
- Ensures auditability and compliance

---

## Data Flow

```text
Input:
- Denial letter (unstructured)
- Patient context (synthetic, FHIR-style)
- Payer policy criteria

Processing:
1. Denial Interpreter extracts structured denial data
2. Clinical Evidence Finder extracts evidence
3. Policy Match compares evidence with criteria
4. Appeal Writer generates structured outputs
5. Safety Agent validates the result

Output:
- Structured appeal packet for clinician review
```

---

## Core Data Structures

### 1. Patient Timeline

Chronological representation of:
- encounters
- therapies
- medications
- findings

---

### 2. Evidence-to-Criteria Matrix

| Payer Criterion | Evidence Found | Source | Status | Gap | Next Action |
|---|---|---|---|---|---|

This is the central reasoning artifact of the system.

---

### 3. Appeal Packet

Includes:
- denial summary
- evidence mapping
- documentation gaps
- appeal strategy
- draft appeal letter
- peer-to-peer brief
- patient explanation
- safety review

---

## A2A Workflow Model

AppealOS uses an Agent-to-Agent coordination model:

- Each agent performs a narrow, well-defined task
- Outputs are passed sequentially between agents
- No single agent performs end-to-end reasoning
- The Orchestrator ensures consistency and completeness

This design improves:
- modularity
- explainability
- auditability

---

## Use of Generative AI

AppealOS uses generative AI for:

- interpreting unstructured denial language
- synthesizing fragmented patient context
- mapping evidence to policy criteria
- generating structured documentation

This enables flexible reasoning beyond rule-based systems.

---

## Safety Architecture

AppealOS enforces strict safety boundaries:

- synthetic or de-identified data only
- no real PHI usage
- no diagnosis or prescribing
- no medical necessity determination
- no autonomous action

The Safety and Compliance Agent acts as a final validation layer.

---

## Auditability

The system is designed to be auditable:

- Each agent produces structured outputs
- Evidence is traceable to sources
- Gaps are explicitly identified
- Reasoning is visible in the matrix

---

## Limitations

- Prototype system using synthetic data
- No integration with live EHR systems
- No real-time payer APIs
- No automated appeal submission
- Requires clinician review before use

---

## Summary

AppealOS uses a modular multi-agent architecture to transform denial workflows into structured, auditable processes.

By combining A2A coordination with generative AI, the system enables evidence-based appeal preparation while maintaining safety and compliance boundaries.
