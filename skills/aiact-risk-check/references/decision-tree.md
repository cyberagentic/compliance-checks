# EU AI Act — Classification Decision Tree

## CLASSIFICATION PRINCIPLE

Conservative. When a step cannot be clearly determined from the available information, assume the higher-risk path. Never default to "Minimal Risk" when information is missing. Each inference must include a one-sentence justification. If a step is genuinely undecidable, mark it as AMBIGUOUS.

---

## Step C1 — Entity Type

Use field: `role` (from Q2)
Source: Article 3 points 2-8

| Value | Tags | Next Step |
|-------|------|-----------|
| provider | AI Literacy | → C2 |
| deployer | AI Literacy | → C2 |
| distributorImporter | (none) | → C2 |
| productManufacturer | (none) | → C3 |

Track `effectiveRole` = `role` value from this point forward. If "Become a Provider" tag is assigned at any later step, set `effectiveRole` = "provider" for all subsequent steps.

## Step C2 — High-Risk Area Check

Use field: `applicationArea` (from Q3)
Source: Article 6 points 1-2, Annex I, Annex III

Evaluate the user's selection against these three tiers:

**Tier A — Annex I Section B (immediate High-risk):**
If option 10 (Transport & Vehicles) is selected:
- Add tag "High-risk"
- If `effectiveRole` is NOT "provider" → add tag "Become a Provider", set `effectiveRole` = "provider"
- → C4

**Tier B — Annex I Section A (High-risk with conformity assessment):**
If option 9 (Medical Devices & Health) OR option 11 (Industrial Safety) is selected:
- INFER: Conservatively assume third-party conformity assessment is required (merging full-tree steps HR2+HR3)
- Add tag "High-risk"
- If `effectiveRole` is NOT "provider" → add tag "Become a Provider", set `effectiveRole` = "provider"
- Mark as inferred: "Third-party conformity assessment conservatively assumed required for [selected category] under Annex I Section A."
- → C4

**Tier C — Annex III areas:**
If any of options 1-8 is selected:
- → C2b (Significant Risk sub-check)

**No match:**
If option 12 (None of the above) is selected:
- → C4

IMPORTANT: Remember whether Annex I categories were selected — this is needed for the GPAI check in C7.

## Step C2b — Significant Risk Check

Source: Article 6 point 3
Input: `significantRisk` (from Q4 — conditional question, only asked for Annex III areas)

| Value | Action | Next Step |
|-------|--------|-----------|
| Makes autonomous decisions or profiles people | Add tag "High-risk". If `effectiveRole` is NOT "provider" → add tag "Become a Provider", set `effectiveRole` = "provider" | → C4 |
| Unsure | Add tag "High-risk". If `effectiveRole` is NOT "provider" → add tag "Become a Provider", set `effectiveRole` = "provider" | → C4 |
| Only prepares information for human decisions | If `effectiveRole` is "provider" → add tag "Notify NCA" | → C4 |

## Step C3 — Product Manufacturer Check

Use field: `applicationArea` (from Q3)
Source: Article 25 point 3, Annex I

Check if the user selected any Annex I category (options 9, 10, or 11):

**If Annex I match:**
- Add tag "Become a Provider", set `effectiveRole` = "provider"
- → C4

**If no Annex I match:**
- Mark as AMBIGUOUS
- Output: "Product manufacturer without Annex I product match. Consult qualified legal counsel for detailed classification."
- → END

## Step C4 — EU Scope

Source: Article 2

**Preset assumption: EU Scope = yes.** This check always assumes the AI system is used in the EU or aimed at EU users. No user input needed.

→ C5

## Step C5 — Prohibited Practices Check

Source: Article 5
Input: Inferred from `systemNameAndDescription`

Check if the system description indicates ANY of these prohibited practices:

1. **Subliminal manipulation** — techniques below consciousness to distort behavior causing significant harm
2. **Exploiting vulnerabilities** — targeting age, disability, or social/economic situation to distort behavior
3. **Biometric categorisation** — categorising individuals based on biometric data to infer race, political opinions, trade union membership, religious beliefs, sex life, or sexual orientation (prohibited sense of Art. 5)
4. **Social scoring** — evaluating or classifying persons based on social behavior or personality characteristics leading to detrimental treatment
5. **Predictive policing** — risk assessments of individuals to predict criminal offences based solely on profiling or personality traits
6. **Facial recognition databases** — creating or expanding facial recognition databases through untargeted scraping
7. **Emotion recognition in workplace/education** — inferring emotions in workplace or educational settings (except medical or safety reasons)
8. **Real-time remote biometric identification** — in publicly accessible spaces for law enforcement (with narrow exceptions)

**If any match → add tag "Prohibited" → END**
**If no match → C6**

Mark as inferred and state which practices were evaluated.

## Step C6 — Transparency Obligations

Use field: `systemFunctions` (from Q5)
Source: Article 50

Direct mapping from user input — no inference needed. Options are role-dependent (see Q5 in SKILL.md).

**Deployer options:**

| Selection | Tag |
|-----------|-----|
| Generating or manipulating image, audio or video content constituting a deep fake | Transparency: Deep Fake |
| Generating or manipulating text published to inform the public on matters of public interest | Transparency: Public Interest Text |
| Emotion recognition or biometric categorisation | Transparency: Emotion & Biometric |
| None of the above | (no transparency tag) |

**Provider / Distributor-Importer / Product Manufacturer options:**

| Selection | Tag |
|-----------|-----|
| Interacting directly with people | Transparency: Natural Persons |
| Generating synthetic audio, image, video or text content | Transparency: Synthetic Content |
| None of the above | (no transparency tag) |

Multiple selections are possible — assign all matching tags.
→ C7

## Step C7 — GPAI / Systemic Risk Check

Source: Article 51
Input: Inferred from `systemNameAndDescription`

Assess whether the AI system is or uses a general-purpose AI model with high-impact capabilities:

**Indicators for GPAI with Systemic Risk:**
- Large-scale foundation model (e.g., GPT-4 class, Gemini, Claude)
- Models trained with total compute above 10^25 FLOPS
- Models with broad general-purpose capabilities across many domains
- Models classified by the EU Commission as having systemic risk

**NOT systemic risk:** Domain-specific or fine-tuned models for a narrow task (e.g., resume screening, customer service chatbot, medical image classifier).

**If systemic risk inferred → add tags "GPAI" and "GPAI with Systemic Risk"**
**If GPAI but not systemic risk → add tag "GPAI"**
**If not GPAI → no tag**

Mark as inferred and state reasoning.
→ END

---

## Warning Signals — Trigger Ambiguous Classification

Mark the classification as AMBIGUOUS when ANY of these conditions apply:

- System description is fewer than 20 words
- Description mentions multiple potentially conflicting use cases (e.g., "HR tool that also does border surveillance")
- Product manufacturer with no clear Annex I product match (Step C3)
- System operates in a domain adjacent to but not clearly within an Annex III area
- EU scope cannot be determined even after inference attempt
- Description is too vague to meaningfully evaluate prohibited practices

When AMBIGUOUS: Do NOT assign Minimal Risk. Output the Ambiguous category with a recommendation to run the full audit.