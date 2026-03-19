# GDPR Quick Check — Dimension Reference

8 compliance dimensions assessed via traffic-light logic (🟢/🟡/🔴).
Conservative principle: When inferring, always lean toward the more critical assessment. A false-GREEN is worse than a false-RED.

---

## Dimension 1 — Personal Data & Categories
**GDPR:** Art. 4(1), Art. 9, Art. 10
**Input:** Q1 (description) + Q2 (data type)

- 🟢 GREEN: "Standard data only" selected AND description confirms only basic contact/account data
- 🟡 YELLOW: "Unsure" selected OR description suggests potentially sensitive data (location tracking, behavioral profiling, children's data)
- 🔴 RED: "Special categories" or "Criminal offence data" selected but no Art. 9(2) exception apparent from context

**Inference guidance:** Assess data categories from the service description. HR tools likely process employee data (potentially health data for sick leave). Marketing tools may process behavioral/profiling data. Educational tools may involve children's data.

---

## Dimension 2 — Legal Basis
**GDPR:** Art. 6(1)
**Input:** Q5 (legal basis) + Q1 (description)

- 🟢 GREEN: Legal basis clearly identified AND plausible for the described purpose (e.g., contract performance for a CRM serving existing customers)
- 🟡 YELLOW: "Legitimate interest" selected (requires documented balancing test) OR legal basis stated but fit is uncertain for the described purpose
- 🔴 RED: "Not yet determined" or "Unsure" selected

⚠️ "Legitimate interest" is NOT automatically GREEN. Without evidence of a documented balancing test, assess as YELLOW.

⚠️ **Consent cross-check:** If "Consent" is selected but the service is an employer-mandated tool, note that consent may not be freely given in an employment context (Art. 7, Recital 43) and assess as YELLOW.

---

## Dimension 3 — DPIA Requirement
**GDPR:** Art. 35
**Input:** Q1 (description) + Q2 (data type) + inference

- 🟢 GREEN: Standard data, no obvious DPIA triggers, small-scale processing
- 🟡 YELLOW: Some risk indicators present (e.g., employee monitoring, customer scoring) but no mandatory Art. 35(3) trigger
- 🔴 RED: Any of the mandatory triggers identified — special categories at scale, systematic monitoring of public areas, profiling with legal effect, scoring/evaluation of individuals

⚠️ **Mandatory DPIA triggers** — if ANY of the following apply, do NOT assess as GREEN:
- Large-scale processing of special categories (Art. 9)
- Systematic monitoring of publicly accessible areas
- Automated individual decision-making with legal/significant effect
- Scoring or systematic evaluation of personal aspects
- Large-scale profiling or tracking

**Inference guidance:** Assess from service type. Surveillance/CCTV platforms, large-scale HR analytics, credit scoring services, health data platforms at scale all trigger DPIA requirements.

---

## Dimension 4 — Data Protection Principles
**GDPR:** Art. 5(1)
**Input:** Q1 (description) — fully inferred

- 🟢 GREEN: Purpose clearly defined and specific, data collection appears proportionate, storage limitation addressable
- 🟡 YELLOW: Purpose broad or vague (e.g., "analytics and improvement"), potential over-collection, unclear retention policies
- 🔴 RED: No clear purpose identifiable, obvious data maximisation (collects far more than needed), or indefinite retention with no justification

**Inference guidance:** Evaluate purpose limitation (is the purpose specific?), data minimisation (does the service collect only what's needed?), and storage limitation (is there a plausible retention concept?). Services with vague "we may use data for any purpose" descriptions lean toward YELLOW/RED.

---

## Dimension 5 — Data Subject Rights
**GDPR:** Art. 15–22
**Input:** Q1 (description) — fully inferred

- 🟢 GREEN: Service type typically supports rights fulfillment (standard SaaS with user accounts, export features, deletion capabilities)
- 🟡 YELLOW: Some rights may be difficult to fulfill (e.g., data portability in proprietary formats, complex data structures making erasure difficult)
- 🔴 RED: Service design fundamentally conflicts with rights (e.g., immutable ledger systems, no data export capability, no user-level data isolation)

**Inference guidance:** Standard SaaS tools with user accounts generally support access, rectification, and erasure. Check for portability (does the service offer data export?). Services that aggregate or anonymize data may complicate access requests.

---

## Dimension 6 — Third Country Transfer
**GDPR:** Art. 44 ff.
**Input:** Q3 (third country transfer) + Q1 (description)

- 🟢 GREEN: Q3 answered "No" AND provider is clearly EU/EEA-based with no indicators of third-country infrastructure
- 🟡 YELLOW: Q3 answered "Yes" (transfer exists but mechanism unknown) OR Q3 answered "No" but provider is a known US/third-country company (cross-check required) OR Q3 answered "Unsure"
- 🔴 RED: Transfer confirmed with no adequate safeguards identifiable from context

⚠️ **"Unsure" on third-country transfer is NOT GREEN.** Many cloud services have US infrastructure or US sub-processors.

⚠️ **US provider cross-check:** If the service is a known US provider (AWS, Azure, Google Cloud, Salesforce, Microsoft 365, Slack, Zoom, HubSpot, Dropbox, etc.) and Q3 was answered "No" — challenge the answer in the comment and assess as YELLOW, not GREEN.

---

## Dimension 7 — Data Processing Agreement
**GDPR:** Art. 28
**Input:** Q4 (DPA status)

- 🟢 GREEN: "Yes, concluded"
- 🟡 YELLOW: "In preparation"
- 🔴 RED: "No" or "Unsure"

⚠️ **A cloud service WITHOUT a DPA is ALWAYS RED.** There is no exception. Art. 28 GDPR is mandatory for any processor relationship.

---

## Dimension 8 — Accountability
**GDPR:** Art. 5(2), Art. 30, Art. 33
**Input:** Q1 (description) — fully inferred

- 🟢 GREEN: Context indicates organisation has processing records and breach procedures in place (e.g., established enterprise with compliance programme)
- 🟡 YELLOW: Unclear whether accountability measures exist, or this is a new service introduction without established documentation
- 🔴 RED: Clear indicators that no accountability measures exist (e.g., no processing records, no breach notification process mentioned despite being required)

**Inference guidance:** For most initial cloud service assessments, YELLOW is the most realistic assessment — accountability measures for the specific new service typically need to be created. Assess GREEN only when there is positive evidence of existing accountability infrastructure.
