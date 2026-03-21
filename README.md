# Compliance Checks

EU regulatory compliance checks for businesses. Covers NIS-2 applicability, EU AI Act risk classification, GDPR risk assessment for new applications and systems, TOM review, and DPA review — producing structured reports against legal requirements.

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
| **nis2-check** | NIS-2 Directive applicability assessment. Determines whether an entity falls within NIS-2 scope and classifies it as essential or important. |
| **aiact-risk-check** | EU AI Act risk classification with simplified decision tree. Determines risk category and maps applicable obligations. |
| **gdpr-risk-check** | GDPR risk check for new applications and systems. Assesses 8 compliance dimensions and determines risk category. |
| **tom-check** | Assesses Technical and Organizational Measures against 12 check points aligned to Art. 32 GDPR and ISO 27001. Accepts PDF, Word, or pasted text. |
| **dpa-check** | Reviews a Data Processing Agreement against 9 mandatory check points from Art. 28 GDPR. Accepts PDF, Word, or pasted text. |

## NIS-2 Check

Assess whether an entity falls within the scope of the NIS-2 Directive (EU 2022/2555).

```
/compliance-checks:nis2-check
```

**What it does:**
1. Gathers entity information: website URL or company name + country, optionally sector, employee count, turnover, balance sheet total
2. Cross-references against NIS-2 scope rules, sector lists (Annex I + II), and size thresholds
3. Produces a classification report: 🔴 essential entity, 🟡 important entity, 🟢 not in scope, or ⚠️ conditional

**Criteria assessed:**
- Sector and sub-sector matching (Annex I high-criticality / Annex II other critical sectors)
- Size thresholds (employees, turnover, balance sheet total)
- Special-rule entities (regardless of size)
- Essential vs. important entity classification

## EU AI Act Check

Classify an AI system under the EU AI Act and map applicable obligations.

```
/compliance-checks:aiact-risk-check
```

**What it does:**
1. Asks 6 intake questions (+ conditional follow-ups): system description, role in AI value chain, application area, significant risk, transparency functions, exclusions
2. Processes a simplified classification decision tree internally (Steps C1–C8)
3. Produces a report with risk category and applicable obligations

**Risk categories:**
- 🔴 Prohibited — Art. 5 EU AI Act
- 🟠 High Risk — Art. 6 EU AI Act
- 🟡 Limited Risk — Art. 50 transparency obligations
- 🟢 Minimal Risk — Art. 4 AI literacy only
- ⚪ Excluded / Not in Scope
- ⚠️ Ambiguous — insufficient information

## GDPR Check

GDPR risk check for introducing a new application or system.

```
/compliance-checks:gdpr-risk-check
```

**What it does:**
1. Asks 5 intake questions: service description, data types, third-country transfer, DPA status, legal basis
2. Assesses 8 compliance dimensions (🟢/🟡/🔴 per dimension)
3. Produces a risk category (🔴 High / 🟡 Limited / 🟢 Minimal) with an obligations table

**Dimensions assessed:**
- Personal data classification
- Legal basis
- DPIA requirement
- Data protection principles
- Data subject rights
- Third country transfer
- Data processing agreement
- Accountability

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

## Example Workflows

### Check NIS-2 applicability for your organisation
Provide a company website or name + country. Get a scope assessment with sector matching, size threshold analysis, and essential/important classification.

### Classify an AI system under the EU AI Act
Describe your AI system and its use case. Get a risk classification and a list of applicable obligations.

### Evaluate a new application for GDPR compliance
Describe the application or system you want to introduce and answer 5 quick questions. Get a risk category with an obligations table showing which dimensions need attention.

### Assess a vendor's TOM documentation
Upload the TOM annex from a processor and check whether all 12 key security areas are adequately documented — from physical security to deletion concepts.

### Review a DPA from a new SaaS vendor
Upload the vendor's Data Processing Agreement and get an Art. 28 GDPR compliance check. Identify missing clauses, incomplete provisions, and critical gaps before signing.

## File Structure

```
compliance-checks/
├── .claude-plugin/
│   └── plugin.json
├── README.md
└── skills/
    ├── nis2-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── nis2-criteria.md
    ├── aiact-risk-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── decision-tree.md
    ├── gdpr-risk-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── gdpr-dimensions.md
    ├── tom-check/
    │   ├── SKILL.md
    │   └── references/
    │       └── check-requirements.md
    └── dpa-check/
        ├── SKILL.md
        └── references/
            └── check-requirements.md
```

## Setup

No external services or environment variables required. The plugin works entirely through Claude's built-in capabilities — upload or paste your documents and get structured compliance reports.
