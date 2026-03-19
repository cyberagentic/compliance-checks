# TOM Quick Check — Requirements Catalog (12 Check Points)

## How to use this reference

Each check point assesses whether the key areas of technical and organizational measures are addressed and adequately described. Check points are ordered following ISO/IEC 27001:2022 Annex A control domains: Organizational (5.x) → People (6.x) → Physical (7.x) → Technological (8.x).

The check uses a 3-level traffic light scale:

- **🟢 GREEN** — Requirement met
- **🟡 YELLOW** — Action needed — topic addressed but incomplete or too generic
- **🔴 RED** — Critical — topic missing or not discernibly regulated

---

## TOM-01 — Data Protection Organization, Training & Certification

- **ISO 27001 Reference:** 5.1–5.4 (Policies, Roles, Segregation, Management), 6.3 (Awareness & Training), 6.6 (Confidentiality Agreements)

### Review Criteria

1. Is a security and data protection organization with assigned responsibilities discernible?
2. Are employees committed to confidentiality and trained on a regular basis?
3. Are data protection requirements considered in development and procurement (Privacy by Design / Default)?
4. Are recognized security certifications in place (e.g., ISO/IEC 27001, SOC 2 Type II)?

### Assessment Criteria

- **🟢 GREEN:** Organization established, training and confidentiality commitments in place, Privacy by Design addressed, certification present.
- **🟡 YELLOW:** Organization in place but gaps (e.g., no training, no Privacy by Design, no certification).
- **🔴 RED:** No discernible security or data protection organization.

---

## TOM-02 — Supplier & Processor Control

- **ISO 27001 Reference:** 5.19–5.23 (Supplier Relationships, Supplier Agreements, ICT Supply Chain, Supplier Monitoring, Cloud Services)

### Review Criteria

1. Is the management of security risks from supplier relationships addressed?
2. Are security requirements contractually agreed with suppliers and sub-processors?
3. Are suppliers and service providers reviewed on a regular basis?
4. Is the handling of cloud services regulated?

### Assessment Criteria

- **🟢 GREEN:** Supplier management with contractual requirements, regular reviews, and cloud governance described.
- **🟡 YELLOW:** Supplier relationships addressed but incomplete.
- **🔴 RED:** No information on supplier or processor control.

---

## TOM-03 — Incident Management & Reporting

- **ISO 27001 Reference:** 5.24–5.28 (Incident Planning, Assessment, Response, Learning, Evidence Collection)

### Review Criteria

1. Is the handling of security incidents regulated?
2. Is a reporting pathway for personal data breaches described?
3. Are lessons learned from security incidents used for improvement?

### Assessment Criteria

- **🟢 GREEN:** Incident management and reporting pathways described, improvement from incidents discernible.
- **🟡 YELLOW:** Topic addressed but incomplete.
- **🔴 RED:** No incident management or reporting pathway discernible.

---

## TOM-04 — Review & Continuous Improvement

- **ISO 27001 Reference:** 5.35–5.36 (Independent Review, Compliance with Policies & Standards)

### Review Criteria

1. Is the effectiveness of measures reviewed on a regular basis?
2. Are independent reviews conducted (e.g., audits)?
3. Is a continuous improvement process discernible?

### Assessment Criteria

- **🟢 GREEN:** Regular effectiveness reviews, independent audits, and improvement process described.
- **🟡 YELLOW:** Reviews mentioned but not regular or not independent.
- **🔴 RED:** No information on review of measures.

---

## TOM-05 — Physical Security

- **ISO 27001 Reference:** 7.1–7.5 (Security Perimeters, Physical Entry, Securing Facilities, Monitoring, Environmental Threats)

### Review Criteria

1. Are measures for the physical protection of premises and facilities described?
2. Is access to security-critical areas regulated?
3. Are protective measures against physical and environmental threats specified?

### Assessment Criteria

- **🟢 GREEN:** Physical security measures concretely described, access restrictions and environmental threat protection addressed.
- **🟡 YELLOW:** Physical security mentioned but key aspects missing or described only in general terms.
- **🔴 RED:** No information on physical security.

---

## TOM-06 — Access Control & Authentication

- **ISO 27001 Reference:** 5.15–5.17 (Access Control, Identity Management, Authentication Information), 8.1 (User Endpoint Devices), 8.5 (Secure Authentication)

### Review Criteria

1. Are measures described that restrict logical access to IT systems to authorized persons?
2. Are appropriate authentication mechanisms in place?
3. Is endpoint protection addressed, including mobile working and remote access?

### Assessment Criteria

- **🟢 GREEN:** Access controls, authentication mechanisms, and endpoint protection described.
- **🟡 YELLOW:** Access control mentioned but authentication or endpoint protection insufficiently described.
- **🔴 RED:** No information on access control or authentication.

---

## TOM-07 — Access Rights Management

- **ISO 27001 Reference:** 5.18 (Access Rights), 8.2 (Privileged Access Rights), 8.3 (Information Access Restriction)

### Review Criteria

1. Are access rights granted following the principle of least privilege?
2. Is the lifecycle of permissions regulated (granting, modification, revocation)?
3. Are permissions reviewed on a regular basis?
4. Is the handling of privileged access rights separately regulated?

### Assessment Criteria

- **🟢 GREEN:** Authorization concept with lifecycle management, regular reviews, and privileged access handling described.
- **🟡 YELLOW:** Permission granting addressed but reviews or privileged access handling insufficiently regulated.
- **🔴 RED:** No discernible authorization concept.

---

## TOM-08 — Separation Control

- **ISO 27001 Reference:** 8.22 (Segregation of Networks), 8.31 (Separation of Development, Test and Production Environments)

### Review Criteria

1. Is separation of data belonging to different controllers or processing purposes ensured?
2. Are production, test, and development environments operated separately?
3. Is network segmentation described?

### Assessment Criteria

- **🟢 GREEN:** Multi-tenancy separation, environment separation, and network segmentation described.
- **🟡 YELLOW:** Separation generally addressed but not all relevant layers covered.
- **🔴 RED:** No information on separation.

---

## TOM-09 — Encryption & Pseudonymization

- **ISO 27001 Reference:** 8.11 (Data Masking), 8.24 (Use of Cryptography)

### Review Criteria

1. Are measures for encryption in transit and at rest described?
2. Is the management of cryptographic keys regulated?
3. Are pseudonymization or anonymization techniques applied where appropriate?

### Assessment Criteria

- **🟢 GREEN:** Encryption measures with key management and pseudonymization described.
- **🟡 YELLOW:** Encryption mentioned but key management or pseudonymization not addressed.
- **🔴 RED:** No information on encryption or pseudonymization.

---

## TOM-10 — Integrity & Transfer Security

- **ISO 27001 Reference:** 5.14 (Information Transfer), 8.12 (Data Leakage Prevention), 8.15 (Logging)

### Review Criteria

1. Are measures for secure data transmission described?
2. Are measures to protect against unintentional or unauthorized data exfiltration specified?
3. Is traceability of data modifications ensured through logging?

### Assessment Criteria

- **🟢 GREEN:** Secure transmission, data exfiltration protection, and logging described.
- **🟡 YELLOW:** Partially addressed but key aspects missing.
- **🔴 RED:** No information on transfer security or traceability.

---

## TOM-11 — Availability & Recovery

- **ISO 27001 Reference:** 5.29–5.30 (Information Security During Disruption, ICT Readiness for Business Continuity), 8.13–8.14 (Information Backup, Redundancy)

### Review Criteria

1. Is a backup and recovery concept described?
2. Are recovery tests conducted?
3. Are measures to ensure availability described (e.g., redundancy, malware protection, vulnerability management)?
4. Is an IT emergency or disaster recovery plan in place?

### Assessment Criteria

- **🟢 GREEN:** Backup concept, recovery tests, availability measures, and IT emergency plan described.
- **🟡 YELLOW:** Basic measures in place but key aspects missing.
- **🔴 RED:** No information on availability or recovery.

---

## TOM-12 — Deletion & Storage Limitation

- **ISO 27001 Reference:** 7.10 (Storage Media), 7.14 (Secure Disposal or Re-use of Equipment), 8.10 (Information Deletion)

### Review Criteria

1. Is the handling of data deletion described?
2. Are retention periods defined?
3. Is the secure disposal of data carriers regulated?
4. Are statutory retention obligations taken into account?

### Assessment Criteria

- **🟢 GREEN:** Deletion, retention periods, secure disposal, and statutory obligations addressed.
- **🟡 YELLOW:** Deletion mentioned but without periods, disposal, or statutory obligations.
- **🔴 RED:** No information on deletion or storage limitation.
