# Compliance Checks

An AI-powered compliance assessment toolkit for data protection and regulatory teams. Automates DPA reviews, TOM assessments, GDPR cloud service checks, and EU AI Act risk classifications — producing structured, traffic-light reports against legal requirements.

**Disclaimer**: This plugin assists with compliance workflows but does not provide legal advice. All assessments should be reviewed by qualified legal professionals. Regulatory requirements change frequently; always verify current requirements with authoritative sources.

## Target Personas

- **Data Protection Officers** — DPA reviews, TOM assessments, GDPR compliance checks
- **Privacy / Compliance Teams** — Vendor assessments, cloud service introductions, regulatory pre-screening
- **In-House Counsel** — Contract review support for data processing agreements, regulatory risk assessment
- **AI Governance Teams** — EU AI Act risk classification, obligations mapping

## Installation

```
claude plugins add cyberagentic/compliance-plugin
```

## Skills

| Skill | Description |
|-------|-------------|
| **dpa-check** | Reviews a Data Processing Agreement against 9 mandatory check points from Art. 28 GDPR. Accepts PDF, Word, or pasted text. |
| **tom-check** | Assesses Technical and Organizational Measures against 12 check points aligned to Art. 32 GDPR and ISO 27001. Accepts PDF, Word, or pasted text. |
| **gdpr-check** | Quick GDPR compliance check for cloud service introductions. Assesses 8 compliance dimensions with traffic-light dashboard. |
| **aiact-risk-check** | EU AI Act risk classification with full decision tree. Determines risk category and maps likely applicable obligations. |

## DPA Check

Review a Data Processing Agreement for Art. 28 GDPR compliance.

```
/compliance-checks:dpa-check
```

**Accepts:** PDF upload, Word/DOCX upload, or pasted contract text.

**What it does:**
1. Asks 3 intake questions: contract input, your role (controller/processor), third-country nexus
2. Evaluates 9 check points strictly aligned to Art. 28 GDPR (Para. 3 lit. a–h + Para. 9)
3. Produces a traffic-light report: 🔴 Critical → 🟡 Action Needed → 🟢 Requirement Met

**Check points covered:**
- Written form and mandatory contract contents
- Documented instructions
- Confidentiality
- Technical and organizational measures
- Sub-processors (authorization, flow-down, liability)
- Data subject rights assistance
- Security and notification obligations
- Deletion and return
- Accountability and audit

## TOM Check

Assess a Technical and Organizational Measures document against Art. 32 GDPR.

```
/compliance-checks:tom-check
```

**Accepts:** PDF upload, Word/DOCX upload, or pasted text (TOM annex, security concept, or standalone TOM description).

**What it does:**
1. Accepts the TOM documentation
2. Evaluates 12 check points ordered by ISO 27001:2022 Annex A domains with GDPR article references
3. Produces a traffic-light report: 🔴 Critical → 🟡 Action Needed → 🟢 Requirement Met

**Check points covered:**
- Data protection organization, training & certification
- Supplier & processor control
- Incident management & reporting
- Review & continuous improvement
- Physical security
- Access control & authentication
- Access rights management
- Separation control
- Encryption & pseudonymization
- Integrity & transfer security
- Availability & recovery
- Deletion & storage limitation

## GDPR Check

Quick GDPR compliance assessment for introducing a cloud service.

```
/compliance-checks:gdpr-check
```

**What it does:**
1. Asks 5 intake questions: service description, data types, third-country transfer, DPA status, legal basis
2. Assesses 8 compliance dimensions with traffic-light ratings
3. Produces a dashboard with overall assessment and prioritized recommendations

**Dimensions assessed:**
- Personal data classification
- Legal basis
- DPIA requirement
- Data protection principles
- Data subject rights
- Third country transfer
- Data processing agreement
- Accountability

## EU AI Act Check

Classify an AI system under the EU AI Act and map likely applicable obligations.

```
/compliance-checks:aiact-risk-check
```

**What it does:**
1. Asks 5 intake questions: system description, role in AI value chain, application area, EU scope, system functions
2. Processes a full classification decision tree internally (Steps I → E1–E3 → HR1–HR6 → S1 → R1–R5)
3. Produces a 3-section report: Risk Classification Record, Likely Applicable Obligations, Recommended Next Steps

**Risk categories:**
- 🔴 Prohibited — Art. 5 EU AI Act
- 🟠 High Risk — Art. 6 EU AI Act
- 🟡 Limited Risk — Art. 50 transparency obligations
- 🟢 Minimal Risk — Art. 4 AI literacy only
- ⚪ Not in Scope
- ⚠️ Ambiguous — insufficient information

## Example Workflows

### Review a DPA from a new SaaS vendor
Upload the vendor's Data Processing Agreement and get an instant Art. 28 GDPR compliance check. Identify missing clauses, incomplete provisions, and critical gaps before signing.

### Assess a vendor's TOM documentation
Upload the TOM annex from a processor and check whether all 12 key security areas are adequately documented — from physical security to deletion concepts.

### Evaluate a new cloud service for GDPR compliance
Describe the cloud service you want to introduce and answer 5 quick questions. Get a compliance dashboard showing which dimensions need attention before deployment.

### Classify an AI system under the EU AI Act
Describe your AI system and its use case. Get a risk classification, a record of the legal assessment, and a list of likely applicable obligations — all in one report.

### Check if a DPA covers third-country transfers
Upload a DPA and indicate there's a third-country nexus. The check applies enhanced scrutiny to instruction binding and sub-processor provisions for international data transfers.

## File Structure

```
compliance-checks/
├── .claude-plugin/
│   └── plugin.json
├── README.md
└── skills/
    ├── dpa-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── check-requirements.md
    ├── tom-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── check-requirements.md
    ├── gdpr-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── gdpr-dimensions.md
    └── aiact-risk-check/
        ├── SKILL.md
        └── references/
            └── decision-tree.md
```

## Setup

No external services or environment variables required. The plugin works entirely through Claude's built-in capabilities — upload or paste your documents and get structured compliance reports.
