---
name: aiact-risk-check
description: "EU AI Act quick risk classification for AI systems. Use when user asks to 'classify AI system', 'EU AI Act check', 'KI-System klassifizieren', 'AI Act Risiko pruefen', 'determine AI risk category', 'quick AI Act assessment'. Accepts system description and determines risk category through simplified decision tree."
license: "Proprietary. See LICENSE.txt for complete terms."
---

# EU AI Act — Quick Risk Classification

You are performing a quick EU AI Act risk classification. This is a lightweight pre-screening that determines the risk category of an AI system through up to 5 questions and a simplified decision tree.

## Preset Assumptions

These apply to every check and are NOT asked:

| Assumption | Value | Reason |
|---|---|---|
| EU Scope | Yes | This check assumes the AI system is used in the EU or aimed at EU users. Systems without EU connection are out of scope for this check. |

## PHASE 1: Intake

Collect the following information. Questions 1-3, 5, and 6 are always asked. Question 4 is conditional (only for Annex III areas). If the user has already provided some answers in their message, extract them and ask only for the missing fields. Present the questions in a clear, numbered format.

Do NOT proceed to Phase 2 until all applicable questions are answered.

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
| Distributor / Importer | Makes an AI system available on the EU market or places it from a third country on the EU market |
| Product Manufacturer | Integrates AI into a product and places the product on the market under its own name or trademark |

### Question 3 — Application Area (Two-Step)

This question uses two steps to stay within the 4-option display limit.

**Step 3a — Category Group**

Ask the user to select ONE group:

| Option | Covers |
|--------|--------|
| People & Society | Biometrics, Law Enforcement, Migration, Justice & Democracy |
| Employment, Education & Services | Education, Employment, Financial & Essential Services |
| Infrastructure & Safety | Critical Infrastructure, Medical Devices, Transport, Industrial Safety |
| None of the above | No high-risk application area |

**Step 3b — Specific Area (only if group selected)**

If the user selected a group in 3a, show the specific areas for that group and ask to select ALL that apply:

*People & Society:*

| # | Option |
|---|--------|
| 1 | Biometrics & Identity Verification |
| 6 | Law Enforcement & Criminal Justice |
| 7 | Migration, Asylum & Border Control |
| 8 | Justice & Democratic Processes |

*Employment, Education & Services:*

| # | Option |
|---|--------|
| 3 | Education & Training |
| 4 | Employment & Workforce Management |
| 5 | Financial & Essential Services (credit, insurance, public benefits) |

*Infrastructure & Safety:*

| # | Option |
|---|--------|
| 2 | Critical Infrastructure (energy, water, transport, digital) |
| 9 | Medical Devices & Health |
| 10 | Transport & Vehicles (aviation, automotive, marine, rail) |
| 11 | Industrial Safety (machinery, explosives, pressure equipment, lifts, PPE) |

If "None of the above" was selected in 3a, map directly to option 12.

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

### Question 4 — Significant Risk (Conditional)

Only ask this question if the user selected an Annex III area in Q3 (options 1-8). If Q3 = "None of the above" or an Annex I area (options 9-11), skip this question.

Ask: "Does the AI system make autonomous decisions that significantly affect people — or does it only prepare information for human decisions?"

| Option | Description |
|--------|-------------|
| Makes autonomous decisions or profiles people | The system decides, scores, ranks, or profiles individuals without meaningful human review |
| Only prepares information for human decisions | The system supports or informs human decision-makers but does not replace them |
| Unsure | It is unclear whether the system acts autonomously |

**Mapping:**
- "Makes autonomous decisions or profiles people" OR "Unsure" → significant risk = yes → High-risk tag
- "Only prepares information" → significant risk = no → No High-risk tag (but add "Notify NCA" tag if effectiveRole is provider)

### Question 5 — Transparency Functions (Role-Dependent)

Show different options depending on the role selected in Q2. This is a **multiple-choice question** — the user may select **more than one option**. Present it explicitly as multi-select (e.g. "Select all that apply — you can choose multiple options"). "None of the above" is mutually exclusive with all other options.

**CRITICAL: Each role has its OWN set of options. You MUST show ONLY the options listed for the user's role. Do NOT mix options across roles. Deployers have DIFFERENT options than Providers. Verify the role from Q2 before presenting options.**

**If Q2 = Deployer:**

| # | Option | Description |
|---|--------|-------------|
| A | Generating or manipulating image, audio or video content constituting a deep fake | e.g., face swaps, synthetic video impersonation |
| B | Generating or manipulating text published to inform the public on matters of public interest | e.g., AI-generated news articles, public information summaries |
| C | Emotion recognition or biometric categorisation | e.g., sentiment analysis from face/voice, biometric sorting |
| D | None of the above | No transparency-relevant functions |

The user may select e.g. "A and C" or "A, B, C". If "D" is selected, no other option may be combined.

**If Q2 = Provider:**

| # | Option | Description |
|---|--------|-------------|
| A | Interacting directly with people | e.g., chatbot, voice assistant, virtual agent |
| B | Generating synthetic audio, image, video or text content | e.g., AI-generated content, text synthesis |
| C | None of the above | No transparency-relevant functions |

The user may select e.g. "A and B". If "C" is selected, no other option may be combined.

**If Q2 = Distributor / Importer or Product Manufacturer:**

| # | Option | Description |
|---|--------|-------------|
| A | Interacting directly with people | e.g., chatbot, voice assistant, virtual agent |
| B | Generating synthetic audio, image, video or text content | e.g., AI-generated content, text synthesis |
| C | None of the above | No transparency-relevant functions |

The user may select e.g. "A and B". If "C" is selected, no other option may be combined.

### Question 6 — Exclusion Categories

Ask the user whether any of the following exclusions apply. Select ONE:

| Option | Description |
|--------|-------------|
| Military or national security | The AI system is used exclusively for military, defence, or national security purposes |
| Research & development | The system is used solely for scientific research and development, before any market placement or deployment |
| Open source | The system is released under a free and open-source licence and is not a high-risk system, prohibited practice, or subject to transparency obligations |
| Personal or non-professional use | The system is used by a natural person in the course of a purely personal non-professional activity |
| None of the above | No exclusion applies |

**Mapping:**
- "Military or national security" → add tag "Excluded" → END (no further classification)
- "Research & development" → add tag "Exclusion: Research" (continue classification but note the exclusion in output)
- "Open source" → add tag "Exclusion: Open Source" (continue classification but note the exclusion in output)
- "Personal or non-professional use" → add tag "Exclusion: Personal Use" (continue classification but note the exclusion in output)
- "None of the above" → no tag, continue normally

---

## PHASE 2: Simplified Classification

Load the decision tree from [references/decision-tree.md](references/decision-tree.md) and walk through each step in order.

**IMPORTANT: Do NOT show the classification walkthrough or decision logic in the chat. Process everything internally and only output the final report.**

### Core Rules

- Walk through each step of the compact decision tree in sequence. Do not skip steps that are on the active path.
- Use the user's answers directly where available (Q2 → C1, Q3 → C2/C3, Q4 → C2b, Q5 → C6, Q6 → C8).
- EU Scope (C4) is always assumed "yes" (preset assumption).
- For steps that require inference (C5, C7): infer the most likely answer from `systemNameAndDescription`. Mark every inferred value explicitly with the reasoning.
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
| "Excluded" tag present | Excluded | ⚪ |
| Any Exclusion tag present (Research, Open Source, Personal Use) | Show classification result BUT add exclusion note | — |
| Any step marked AMBIGUOUS or genuinely undecidable | Ambiguous | ⚠️ |

Priority order: Excluded > Prohibited > High Risk > Ambiguous > Limited Risk > Minimal Risk > Not in Scope.

---

## Output

```markdown
## EU AI Act — Risk Classification

---

### Risk Category according EU AI Act: [Symbol] **[Category]**

[2-3 sentences explaining what this classification means in practice:

- If PROHIBITED: "This system likely falls under prohibited AI practices (Art. 5 EU AI Act). Operation should be ceased immediately and qualified legal counsel should be consulted."

- If HIGH RISK: "This system is classified as high-risk under Art. 6 EU AI Act. Consult qualified legal counsel for detailed obligations."

- If LIMITED RISK: "This system has transparency obligations under Art. 50 EU AI Act. [State the specific transparency obligation in one sentence based on the transparency tags assigned.]"

- If MINIMAL RISK: "This system falls under minimal risk. The only applicable obligation is AI literacy (Art. 4 EU AI Act)."

- If NOT IN SCOPE: "The EU AI Act does not apply to this system based on the information provided."

- If AMBIGUOUS: "The available information is insufficient for a definitive risk classification. Consult qualified legal counsel to determine the exact risk category and applicable obligations."]

---

### Applicable Obligations

| Obligation | Article | Description |
|------------|---------|-------------|
| [For each obligation from the Tag → Obligations mapping, add a row] |

[Include EVERY obligation from ALL tags assigned during classification. Use the Tag → Obligations mapping below.]

---

This report has no legal validity.
```

### Tag → Obligations Mapping

For each tag assigned during classification, include the corresponding obligations as bullet points in the "Applicable Obligations" section.

**"AI Literacy":**
- Art. 4 EU AI Act | AI literacy | Take measures to ensure a sufficient level of AI literacy for staff and other persons dealing with the operation and use of AI systems on your behalf.

**"Become a Provider":**
- Art. 25 EU AI Act | Provider role assumption | You are considered a provider for the purposes of this legislation due to modifications or product integration. You must assume full provider obligations accordingly.

**"High-risk" (effectiveRole = provider):**
- Art. 16 EU AI Act | Provider obligations for high-risk AI | Comply with all provider obligations for high-risk AI systems under Article 16
- Art. 9 EU AI Act | Risk management system | Establish, implement, document, and maintain a risk management system
- Art. 10 EU AI Act | Data governance | Ensure training, validation, and testing data meets quality criteria
- Art. 11 EU AI Act | Technical documentation | Draw up technical documentation before placing on market
- Art. 12 EU AI Act | Record-keeping | Ensure automatic logging capabilities
- Art. 13 EU AI Act | Transparency and information | Ensure sufficient transparency for deployers to interpret output
- Art. 14 EU AI Act | Human oversight | Design system to allow effective human oversight
- Art. 15 EU AI Act | Accuracy, robustness, cybersecurity | Ensure appropriate levels of accuracy, robustness, and cybersecurity
- Art. 17 EU AI Act | Quality management system | Establish a quality management system
- Art. 47 EU AI Act | EU Declaration of Conformity | Draw up an EU declaration of conformity
- Art. 48 EU AI Act | CE marking | Affix CE marking to the high-risk AI system
- Art. 49 EU AI Act | Registration | Register the system in the EU database before placing on market or putting into service

**"High-risk" (effectiveRole = deployer):**
- Art. 26 EU AI Act | Deployer obligations for high-risk AI | Comply with all deployer obligations for high-risk AI systems under Article 26

**"High-risk" (effectiveRole = distributorImporter):**
- Art. 23 EU AI Act | Importer obligations for high-risk AI | Comply with all importer obligations under Article 23
- Art. 24 EU AI Act | Distributor obligations for high-risk AI | Comply with all distributor obligations under Article 24

**"Notify NCA" (ONLY applicable when effectiveRole = provider):**
- Art. 49(2) EU AI Act | Registration in EU database | Register the system in the EU database before placing on market or putting into service
- Art. 6(4) EU AI Act | Documentation of assessment | Document the assessment that the system does not pose a significant risk and provide this documentation to the NCA upon request
- **Do NOT assign this tag if the entity is a deployer, distributor, importer, or product manufacturer.**

**"GPAI":**
- Art. 53 EU AI Act | GPAI model obligations | Comply with general-purpose AI model obligations: technical documentation, information to downstream providers, copyright compliance, and transparency.

**"GPAI with Systemic Risk":**
- Art. 55 EU AI Act | Systemic risk obligations | Perform model evaluations, assess and mitigate systemic risks, report serious incidents, and ensure adequate cybersecurity

**"Transparency: Natural Persons":**
- Art. 50(1) EU AI Act | Transparency towards users | Inform users that they are interacting with an AI system

**"Transparency: Synthetic Content":**
- Art. 50(2) EU AI Act | Synthetic content marking | Mark AI-generated content in a machine-readable format and ensure it is detectable as artificially generated

**"Transparency: Content Resemblance":**
- Art. 50(4) EU AI Act | Content resemblance disclosure | Disclose that content has been artificially generated or manipulated to resemble existing persons, objects, places, or events

**"Transparency: Emotion & Biometric":**
- Art. 50(3) EU AI Act | Emotion/biometric/public interest transparency | Inform persons exposed to emotion recognition or biometric categorisation systems, or inform the public that text was generated or manipulated by AI

**"Prohibited":**
- Art. 5 EU AI Act | Prohibited practice | Your system may be prohibited under the EU AI Act. Cease operation or consult legal counsel.

**"Out of scope":**
- Art. 2 EU AI Act | Outside scope | Your system falls outside the territorial or material scope of the EU AI Act.

**"Excluded":**
- Art. 2 EU AI Act | Military/national security exclusion | This system is excluded from the EU AI Act as it is used exclusively for military, defence, or national security purposes.

**"Exclusion: Research":**
- Art. 2(6) EU AI Act | Research exclusion | This system may be excluded from most obligations as it is used solely for scientific research and development prior to market placement. Verify with legal counsel whether the exclusion conditions are fully met.

**"Exclusion: Open Source":**
- Art. 2(12) EU AI Act | Open-source exclusion | This system may benefit from reduced obligations under the open-source exclusion. Note: this exclusion does NOT apply if the system is classified as high-risk, prohibited, or subject to transparency obligations. Verify with legal counsel.

**"Exclusion: Personal Use":**
- Art. 2(10) EU AI Act | Personal use exclusion | This system may be excluded as it is used by a natural person in a purely personal, non-professional capacity. Verify with legal counsel.

### Output Rules

- Do NOT add disclaimers or general EU AI Act explanations beyond the template.
- Do NOT add traffic-light groupings, decision paths, or result tables.
- List ALL applicable obligations based on ALL tags assigned during classification.
- **ONLY include obligations that are explicitly listed in the Tag → Obligations mapping above. Do NOT invent, paraphrase, soften, or add "advisory" obligations that are not in the mapping. If a tag was not assigned, its obligations MUST NOT appear in the output.**
- Each obligation row uses the format: `| Art. X EU AI Act | Title | Description |`
- Keep the output to: header, risk category with explanation, applicable obligations, and note.