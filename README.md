# Compliance Checks

Regulatory compliance assessment toolkit — structured GDPR/DSGVO data protection checks, DPA audits against Art. 28 GDPR, and EU AI Act risk classification.

## Components

### Skills

| Skill | Description |
|-------|-------------|
| **eu-ai-act-check** | Classifies AI systems through a legal decision tree (Articles 2-6, 50 EU AI Act) and generates a compliance report with risk category, obligations, and next steps. |
| **gdpr-check** | Assesses GDPR/DSGVO compliance for cloud service introductions. Classifies data protection obligations and generates a professional assessment report. |
| **dpa-check** | Reviews a Data Processing Agreement (DPA) against 34 requirements derived from Art. 28 GDPR. Accepts PDF, Word, or pasted text and produces a structured audit report with GREEN/YELLOW/RED/BLUE assessments. |

## Usage

### EU AI Act Check

Trigger phrases: "check EU AI Act compliance", "classify an AI system", "determine AI risk category", "assess AI Act obligations"

The skill walks through a structured assessment:
1. Collects information about the AI system (name, description, entity type, etc.)
2. Classifies the system through the EU AI Act decision tree
3. Generates a report with risk category, applicable obligations, and recommended next steps

Supports both German (`de`) and English (`en`) reports.

### GDPR/DSGVO Check

Trigger phrases: "check GDPR compliance", "run a DSGVO check", "assess data protection for a cloud service"

The skill performs a structured data protection assessment:
1. Collects information about the cloud service and its data processing
2. Classifies obligations through the DSGVO decision tree
3. Generates a 12-section professional compliance report

Default report language is German; English is also supported.

### DPA Check

Trigger phrases: "check a DPA", "review a data processing agreement", "audit an Auftragsverarbeitungsvertrag", "assess DPA compliance"

The skill audits a Data Processing Agreement:
1. Accepts the DPA as PDF, Word upload, or pasted text
2. Evaluates 34 requirements across categories (Contractual Foundations, Instruction Binding, Confidentiality, TOMs, Sub-Processors, Data Subject Rights, Deletion, Audit, International Transfers, Liability, Organization)
3. Applies a three-tier system (mandatory/control/governance) with tier-specific assessment rules
4. Generates a structured report with executive summary, critical findings, and prioritized next steps

Default report language is German; English is also supported.

## Setup

No external services or environment variables required. The plugin works entirely through Claude's built-in capabilities.
