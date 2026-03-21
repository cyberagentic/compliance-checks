# EU AI Act — Classification Decision Tree

## CLASSIFICATION PRINCIPLE

Conservative. When a step cannot be clearly determined from the available information, assume the higher-risk path. Never default to "Minimal Risk" when information is missing. Each inference must include a one-sentence justification. If a step is genuinely undecidable, mark it as AMBIGUOUS.

---

## Step C1 — Entity Type

Use field: `role` (from Q2)
Source: Article 3 points 2-8

| Value | Tags | Next Step |
|-------|------|-----------|
| provider | AI Literacy | → C1b |
| deployer | AI Literacy | → C1b |
| distributorImporter | (none) | → C1b |
| productManufacturer | (none) | → C3 |
| authorisedRepresentative | Authorised Representative | → END |

Track `effectiveRole` = `role` value from this point forward. If "Become a Provider" tag is assigned at any later step, set `effectiveRole` = "provider" for all subsequent steps.

## Step C1b — System Modifications

Use field: `systemModifications` (from Q2b — conditional, only for provider/deployer/distributorImporter)
Source: Article 25 points 1-2

If this step does not apply (role is productManufacturer or authorisedRepresentative): skip → C2

If any modification is selected (rebranding, changedPurpose, substantialModification):
- If `effectiveRole` = "provider" → add tag "Handover"
- If `effectiveRole` ≠ "provider" → add tag "Become a Provider", set `effectiveRole` = "provider"
- → C2

If "None of the above" or step skipped:
- → C2

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
| Only prepares information for human decisions | **ONLY if `effectiveRole` = "provider":** add tag "Notify NCA". **If `effectiveRole` is deployer, distributorImporter, or productManufacturer: do NOT add any tag — no "Notify NCA", no "High-risk".** | → C4 |

**Inference guidance when `significantRisk` is null or undetermined:**

If the user did not answer Q4 (value is null), INFER from `systemNameAndDescription` using these criteria from Article 6(3):

The system does NOT pose a significant risk if **ANY** of the following conditions is fulfilled (Art. 6(3)):
- It is intended to perform a narrow procedural task
- It is intended to improve the result of a previously completed human activity
- It is intended to detect decision-making patterns or deviations without replacing or influencing human assessment without proper review
- It is intended to perform a preparatory task to an assessment relevant for the Annex III use cases

**EXCEPTION:** The system is ALWAYS considered to pose a significant risk if it performs **profiling of natural persons** as defined in Article 4(4) GDPR — regardless of the above criteria.

If the criteria cannot be clearly evaluated from the description → assume significant risk (conservative principle).

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

**CRITICAL: Use ONLY the mapping table that matches the user's role from Q2. A Deployer can NEVER receive "Transparency: Natural Persons" or "Transparency: Synthetic Content" tags — those are Provider-only. A Provider can NEVER receive "Transparency: Content Resemblance" or "Transparency: Emotion & Biometric" tags — those are Deployer-only.**

**Deployer options:**

| Selection | Tag |
|-----------|-----|
| Generating or manipulating image, audio or video content constituting a deep fake | Transparency: Content Resemblance |
| Generating or manipulating text published to inform the public on matters of public interest | Transparency: Emotion & Biometric |
| Emotion recognition or biometric categorisation | Transparency: Emotion & Biometric |
| None of the above | (no transparency tag) |

**Provider / Distributor-Importer / Product Manufacturer options:**

| Selection | Tag |
|-----------|-----|
| Interacting directly with people | Transparency: Natural Persons |
| Generating synthetic audio, image, video or text content | Transparency: Synthetic Content |
| None of the above | (no transparency tag) |

Multiple selections are possible — assign all matching tags.
→ C6b

## Step C6b — Public Body Assessment

Source: Article 27, Recital 96
Input: `publicBody` (from Q5b — conditional, only for deployers with High-risk tag)

If this step does not apply (effectiveRole ≠ deployer OR "High-risk" tag not assigned): skip → C7

| Value | Tags | Next Step |
|-------|------|-----------|
| Yes | Fundamental Rights Impact Assessment | → C7 |
| No | (none) | → C7 |

If not asked (skipped due to conditions): → C7

## Step C7 — GPAI / Systemic Risk Check

Source: Article 51
Input: Inferred from `systemNameAndDescription` and `effectiveRole`

**CRITICAL DISTINCTION:** GPAI model obligations (Art. 53, 55) apply ONLY to the **provider of the GPAI model itself** — the entity that develops or trains the foundation model and places it on the market. They do NOT apply to downstream providers or deployers who **build applications on top of** a GPAI model (e.g., a chatbot using the GPT-4 API, a tool powered by Claude). Using a GPAI model via API does not make the system provider a GPAI model provider.

**Step 1 — Is the entity itself the provider of a GPAI model?**

Indicators that the entity IS a GPAI model provider:
- Develops, trains, or fine-tunes a foundation model and makes it available to others
- Places a general-purpose AI model on the EU market (e.g., via API, download, or licensing)
- Examples: OpenAI (GPT-4), Anthropic (Claude), Google (Gemini), Meta (Llama)

Indicators that the entity is NOT a GPAI model provider (just a downstream user):
- Builds an application or product that calls a third-party model via API
- Deploys, integrates, or wraps an existing model without modifying it at the model level
- Examples: a customer service chatbot using GPT-4 API, a medical tool powered by Claude, a content generator using Llama

**If not a GPAI model provider → no GPAI tags → C8**

**Step 2 — Systemic risk assessment (only if GPAI model provider):**

**Indicators for Systemic Risk:**
- Large-scale foundation model (e.g., GPT-4 class, Gemini, Claude)
- Models trained with total compute above 10^25 FLOPS
- Models with broad general-purpose capabilities across many domains
- Models classified by the EU Commission as having systemic risk

**NOT systemic risk:** Domain-specific or narrowly fine-tuned models, even if made available to others.

**If systemic risk inferred → add tags "GPAI" and "GPAI with Systemic Risk"**
**If GPAI model provider but not systemic risk → add tag "GPAI"**

Mark as inferred and state reasoning.
→ C8

## Step C8 — Exclusion Categories

Use field: `exclusions` (from Q6)
Source: Article 2

| Value | Tags | Next Step |
|-------|------|-----------|
| Military or national security | Excluded | → END |
| Law enforcement cooperation with third country | Excluded | → END |
| Research & development | Exclusion: Research | → END |
| Open source | Exclusion: Open Source | → END |
| Personal or non-professional use | Exclusion: Personal Use | → END |
| None of the above | (none) | → END |

**"Excluded" (military/national security OR law enforcement third country) overrides all other tags — the system is fully out of scope.**

**"Exclusion: Research", "Exclusion: Open Source", and "Exclusion: Personal Use" are conditional exclusions.** The classification result still applies, but the output must note that the exclusion may limit or remove obligations depending on the specific circumstances. These exclusions have nuances (e.g., open-source exclusion does NOT apply if the system is high-risk or prohibited), so the report must recommend verifying with legal counsel.

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