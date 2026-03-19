---
name: euaiact-check
description: "EU AI Act quick risk classification for AI systems. Use when user asks to 'classify AI system', 'EU AI Act check', 'KI-System klassifizieren', 'AI Act Risiko pruefen', 'determine AI risk category', 'quick AI Act assessment'. Accepts system description and determines risk category through simplified decision tree."
---

# EU AI Act — Quick Risk Classification

You are performing a quick EU AI Act risk classification. This is a lightweight pre-screening that determines the risk category of an AI system through 5 questions and a simplified decision tree.

## PHASE 1: Intake

Collect exactly 5 pieces of information. If the user has already provided some in their message, extract them and ask only for the missing fields. Present the questions in a clear, numbered format.

Do NOT proceed to Phase 2 until all 5 questions are answered.

### Question 1 — System Name and Description

Ask the user to provide:
- The name of the AI system
- A description of what it does, how it works, and what it is used for

This is the primary source for all inference in subsequent steps. Encourage the user to be specific — the more detail, the more accurate the classification.

### Question 2 — Role in the AI Value Chain

Ask the user to select ONE:

| Option | Description |
|--------|-------------|
| Provider | Develops or has an AI system developed and places it on the market or puts it into service under its own name or trademark |
| Deployer | Uses an AI system under its authority (except for personal non-professional use) |
| Distributor | Makes an AI system available on the market without being provider or importer |
| Importer | Places an AI system from a third country on the EU market |
| Product Manufacturer | Integrates AI into a product and places the product on the market under its own name or trademark |

### Question 3 — Application Area

Ask the user to select ALL that apply:

| # | Option |
|---|--------|
| 1 | Biometrics & Identity Verification |
| 2 | Critical Infrastructure (energy, water, transport, digital) |
| 3 | Education & Training |
| 4 | Employment & Workforce Management |
| 5 | Financial & Essential Services (credit, insurance, public benefits) |
| 6 | Law Enforcement & Criminal Justice |
| 7 | Migration, Asylum & Border Control |
| 8 | Justice & Democratic Processes |
| 9 | Medical Devices & Health |
| 10 | Transport & Vehicles (aviation, automotive, marine, rail) |
| 11 | Industrial Safety (machinery, explosives, pressure equipment, lifts, PPE) |
| 12 | None of the above |

**Internal mapping (do not show to user):**

| Option | Maps to | EU AI Act Reference |
|--------|---------|---------------------|
| 1 | `biometrics` | Annex III |
| 2 | `criticalInfrastructure` | Annex III |
| 3 | `educationTraining` | Annex III |
| 4 | `employment` | Annex III |
| 5 | `essentialServices` | Annex III |
| 6 | `lawEnforcement` | Annex III |
| 7 | `migrationAsylumBorder` | Annex III |
| 8 | `justiceAndDemocracy` | Annex III |
| 9 | `medicalDevices` | Annex I Section A |
| 10 | `civilAviationSecurity`, `motorVehicles`, `marineEquipment`, `railSystems`, `twoThreeWheelVehicles`, `agriculturalForestryVehicles` | Annex I Section B |
| 11 | `machinery`, `lifts`, `explosiveAtmospheres`, `pressureEquipment`, `personalProtectiveEquipment`, `toys`, `recreationalCraft`, `radioEquipment`, `cablewayInstallations`, `gaseousFuels` | Annex I Section A |
| 12 | `none` | — |

### Question 4 — EU Scope

Ask: "Is the AI system used in the EU or aimed at EU users?"

| Option | Meaning |
|--------|---------|
| Yes | System is deployed in the EU, targets EU users, or its output is used in the EU |
| No | System has no EU connection |
| Unsure | EU connection is unclear |

### Question 5 — System Functions

Ask the user to select ALL that apply:

| Option | Description |
|--------|-------------|
| Interacts directly with people | e.g., chatbot, voice assistant, virtual agent |
| Generates or manipulates images, audio, video, or text | e.g., content generation, deepfakes, text synthesis |
| Performs emotion recognition or biometric categorization | e.g., sentiment analysis from face/voice, biometric sorting |
| None of the above | No transparency-relevant functions |

---

## PHASE 2: Simplified Classification

Load the compact decision tree from [references/decision-tree-compact.md](references/decision-tree-compact.md) and walk through each step in order.

### Core Rules

- Walk through each step of the compact decision tree in sequence. Do not skip steps that are on the active path.
- Use the user's answers directly where available (Q2 → C1, Q3 → C2/C3, Q4 → C4, Q5 → C6).
- For steps that require inference (C2b, C5, C7, and parts of C2/C3/C4): infer the most likely answer from `systemNameAndDescription`. Mark every inferred value explicitly with the reasoning.
- Track `effectiveRole` (starts as Q2 value, may change to "provider" if "Become a Provider" tag is assigned).
- Track `inferredCount` (number of values inferred from description).
- Track `totalSteps` (total steps evaluated).

### CRITICAL: Conservative Inference Principle

When inferring values from the system description, ALWAYS classify toward higher risk when uncertain. A false "Minimal Risk" classification is more dangerous than a false "High Risk" classification. When in doubt, output the Ambiguous category: "⚠️ Not clearly classifiable with the available information. Consult qualified legal counsel."

### Risk Category Determination

Based on the collected tags, assign the final risk category:

| Condition | Category | Symbol |
|-----------|----------|--------|
| "Prohibited" tag present | Prohibited | 🔴 |
| "High-risk" tag present | High Risk | 🟠 |
| Any Transparency tag present (but no High-risk or Prohibited) | Limited Risk | 🟡 |
| No risk-relevant tags | Minimal Risk | 🟢 |
| "Out of scope" tag present | Not in Scope | ⚪ |
| Any step marked AMBIGUOUS or genuinely undecidable | Ambiguous | ⚠️ |

Priority order: Prohibited > High Risk > Ambiguous > Limited Risk > Minimal Risk > Not in Scope.

---

## PHASE 3: Output

Generate the report in English. Use the following format exactly:

```
## EU AI Act — Quick Classification

**AI System:** [Name extracted from Q1]
**Role:** [Entity Type from Q2, use display label: Provider/Deployer/Distributor/Importer/Product Manufacturer]
**Date:** [current date]

### Risk Category

[Symbol] **[Category]**

[2-3 sentences explaining what this classification means in practice:

- If PROHIBITED: "This system likely falls under prohibited AI practices (Art. 5 EU AI Act). Operation should be ceased immediately and qualified legal counsel should be consulted."

- If HIGH RISK: "This system is classified as high-risk under Art. 6 EU AI Act. Key obligation areas include [name 2-3 most relevant: risk management system, technical documentation, conformity assessment, human oversight, data governance]. Consult qualified legal counsel for detailed obligations."

- If LIMITED RISK: "This system has transparency obligations under Art. 50 EU AI Act. [State the specific transparency obligation in one sentence based on the transparency tags assigned.]"

- If MINIMAL RISK: "This system falls under minimal risk. The only applicable obligation is AI literacy (Art. 4 EU AI Act)."

- If NOT IN SCOPE: "The EU AI Act does not apply to this system based on the information provided."

- If AMBIGUOUS: "The available information is insufficient for a definitive risk classification. Consult qualified legal counsel to determine the exact risk category and applicable obligations."]

### Decision Path

[Compact representation of the path taken through the decision tree.
Maximum 5-8 lines. Each line follows the format:

Step Name → [Answer or ⚠️ Inferred: brief reasoning] → Result

Example:
C1 Entity Type → Provider → AI Literacy tag
C2 High-Risk Area → Employment (Annex III) → C2b
C2b Significant Risk → ⚠️ Inferred: CV screening with automated ranking constitutes profiling → High-risk tag
C4 EU Scope → Yes → Continue
C5 Prohibited Practices → ⚠️ Inferred: No prohibited practices identified → Continue
C6 Transparency → Interacts with people → Transparency: Natural Persons tag
C7 GPAI → ⚠️ Inferred: Domain-specific model, not GPAI → No tag]

### Note

This quick classification is based on [totalSteps] of 8 possible decision steps. [inferredCount] values were inferred from the system description (⚠️). For a detailed obligations catalog and audit-grade assessment, consult qualified legal counsel.
```

### Output Rules

- Do NOT include an obligations table. Obligations belong in the full audit.
- Do NOT add disclaimers or general EU AI Act explanations beyond the template.
- Do NOT reference internal step identifiers (C1, C2b, etc.) in the Decision Path — use descriptive step names instead (Entity Type, High-Risk Area, etc.).
- Keep the Decision Path to a maximum of 8 lines.
- Always include the recommendation to consult qualified legal counsel in the Note section.

---

## Quality Check

Before generating output, verify all of the following:

1. **Conservative inference**: If any inferred value could reasonably go either way, was the higher-risk option chosen?
2. **Inferred value disclaimer**: If 3 or more values were inferred, add the following line after the Note: "Due to multiple inferred values, consulting qualified legal counsel is recommended for a definitive classification."
3. **High-risk keyword scan**: If the system description mentions ANYTHING related to biometrics, law enforcement, employment, education, critical infrastructure, or health — verify that the High-Risk path (C2/C2b) was properly evaluated.
4. **Prose accuracy**: Does the risk category summary accurately reflect the determined category without overstating certainty?
5. **Ambiguous safety net**: If any step was genuinely undecidable, is the final category Ambiguous (not Minimal Risk)?
