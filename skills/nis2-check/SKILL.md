---
name: nis2-check
description: "NIS-2 Directive applicability check. Determines whether an entity is in scope and classifies it as essential or important."
license: "Proprietary. See LICENSE.txt for complete terms."
---

# NIS-2 Applicability Check

This skill assesses whether a given entity falls within the scope of EU Directive 2022/2555 (NIS-2) and, if so, classifies it as an **essential** or **important** entity.

## Reference Data

Before performing any assessment, read the compressed NIS-2 criteria:
→ `references/nis2-criteria.md`

This file contains the authoritative scope rules, sector lists (Annex I + II), size thresholds, exceptions, and the decision flowchart you must follow.

For sector matching in manufacturing and health/pharma, consult the detailed NACE code reference:
→ `references/nis2-nace-rev2.md`

This file contains the complete NACE Rev. 2 class-level breakdown for all divisions referenced by NIS-2 (C21, C26–C30). Use it to match an entity's specific economic activities to the correct NACE class and NIS-2 Annex sector.

---

## Workflow

### Step 1 — Gather Entity Information

The user provides a **company website URL** (preferred). If the user only provides a company name or description without a URL, ask them for the website URL first. If they cannot provide a URL, fall back to manual intake — ask the user to provide at minimum:
- Entity name
- Country
- Main business activity / sector
- Number of employees OR annual turnover (€)

In manual intake mode, work exclusively with the data provided by the user. Do not use `web_search` or `web_fetch` to look up additional information.

They may **optionally** also provide:
- Annual turnover (€)
- Annual balance sheet total (€)

**If a website URL is provided**, use `web_fetch` to browse the entity's website and gather information about: country, business activities, products/services, and employee count. Explore relevant pages (homepage, about, impressum, etc.).

**Extract or infer the following data points (these are the only fields needed for the Entity Profile):**

| Data Point | Source |
|---|---|
| Entity name | User input |
| Country | Website (impressum / registered address — country only) or user input |
| Main activity | Website (infer from products, services, self-description) |
| Sector & subsector mapping | Infer from activity → match to Annex I / Annex II categories |
| Entity size | Employee count + turnover from website or user input. Turnover rarely on websites — mark as UNKNOWN unless provided. If entity is a subsidiary, note that the parent group's size may apply. |

**Important inference rules:**
- Be transparent about what is inferred vs. what is stated. Always label assumptions clearly.
- When the main activity could map to multiple sectors, list all plausible mappings and note the ambiguity.
- If employee count is not findable, explain that the user needs to provide it for a definitive size assessment, but still proceed with the sector analysis.
- If the website provides insufficient information overall, state clearly what is missing and provide the analysis conditionally. Prompt the user to supply the missing data.
- Only extract the 5 data points listed above. Do not include legal form, registration numbers, VAT IDs, management names, board members, or detailed address information in the Entity Profile — these are not needed for the NIS-2 scope assessment.

### Step 2 — Assess Scope Applicability

Follow the decision flowchart from `references/nis2-criteria.md` Section 7 strictly:

1. **Sector match**: Does the entity's main activity fall within any Annex I or Annex II sector? Map the activity to specific sector → subsector → entity type. Be precise — quote the matching entity type definition from the extract. If the entity operates across multiple sectors (e.g., an energy company with a logistics arm), assess each activity separately — the entity is in scope if ANY of its activities triggers NIS-2. Non-EU entities are in scope if they provide services within the EU; they must designate a representative in the EU.

2. **Size threshold check**: Does the entity meet the medium-sized enterprise threshold?
   - ≥ 50 employees, OR
   - Annual turnover > €10 million, OR
   - Annual balance sheet total > €10 million

   If unknown, clearly state what information is missing and provide conditional conclusions (e.g., "IF the entity has ≥50 employees, THEN…"). For holding companies and groups, the parent company's size may pull a smaller subsidiary into scope; conversely, Member States may consider independence of network/information systems. Entities just below size thresholds may still be designated by Member States under Article 2(2)(b)-(e) special criteria — flag this possibility.

3. **Size-independent check**: Does Article 2(2)–(4) apply? Check whether the entity is:
   - A telecom network/service provider
   - A trust service provider
   - A TLD registry or DNS service provider
   - A domain name registration service provider
   - A sole provider of a critical service
   - A critical entity under the CER Directive
   - A central/regional government public administration entity

   If yes → in scope regardless of size.

4. **Exclusion check**: Does any exclusion apply?
   - Predominantly national security / defence / law enforcement activities
   - Covered by DORA (financial sector entities under Regulation 2022/2554). If DORA applies, NIS-2 risk management and reporting obligations are replaced by DORA — but the entity remains in the NIS-2 cooperation framework.
   - Diplomatic/consular missions

### Step 3 — Classify as Essential or Important

If the entity is in scope, determine classification per Article 3 rules in the extract (Section 4):

- **Essential** if: Large Annex I entity, OR qualified trust service / TLD / DNS provider, OR medium-sized telecom provider, OR central government, OR critical entity under CER, OR Member State special designation
- **Important** if: In scope but does not meet any essential entity criterion

### Classification Scale (Traffic Light)

| Classification | Symbol | Meaning |
|---|---|---|
| Essential Entity | 🔴 | In scope as essential entity — full NIS-2 obligations, stricter supervision |
| Important Entity | 🟡 | In scope as important entity — NIS-2 obligations, lighter supervision |
| Not in Scope | 🟢 | Not subject to NIS-2 |
| Conditional | ⚠️ | Classification depends on missing information — provide data for definitive result |

### Step 4 — Produce the Assessment Report

Output a structured English-language report with the following sections:

```
## NIS-2 Applicability Assessment

### NIS-2 Applicability: [Symbol] [Classification]

**Confidence:** HIGH / MEDIUM / LOW

[2-3 sentences explaining what this classification means in practice. Use softened language ("is likely classified as", "would likely qualify as") rather than definitive statements.
- If ESSENTIAL (🔴): "Based on the available information, this entity is likely classified as an essential entity under NIS-2. Full obligations would apply, including stricter supervision (ex ante + ex post) and higher fines (up to €10M or 2% global turnover)."
- If IMPORTANT (🟡): "Based on the available information, this entity is likely classified as an important entity under NIS-2. NIS-2 obligations would apply with lighter supervision (ex post only) and lower fines (up to €7M or 1.4% global turnover)."
- If NOT IN SCOPE (🟢): "Based on the available information, this entity likely does not fall within the scope of the NIS-2 Directive."
- If CONDITIONAL (⚠️): "The classification depends on missing information. Provide the requested data for a definitive assessment."]

### Entity Profile

| Field | Value |
|---|---|
| Entity name | [name from impressum or user input] |
| Country | [country] |
| Main activity | [description] |
| Sector mapping | [Annex I/II sector → subsector → entity type] |
| Entity size | [employees, turnover or "Unknown — user input required"] |

### Reasoning Summary

[2-3 sentence plain-English summary of why the entity is or is not in scope]

### Applicability Analysis

#### 1. Sector Match

| Activity | Annex Sector | NACE Code |
|---|---|---|
| [entity activity] | [Annex I/II sector reference] | [code] |

[1-2 sentences explaining the mapping]

#### 2. Size Assessment

| Threshold | Required | Actual | Met |
|---|---|---|---|
| Medium-sized (in-scope) | ≥ 50 employees OR turnover > €10M | [entity data] | ✅ / ❌ / UNKNOWN |
| Large enterprise | ≥ 250 employees OR turnover > €50M | [entity data] | ✅ / ❌ / UNKNOWN |

[1-2 sentences on classification logic]

#### 3. Size-Independent Criteria & Exclusions

If ALL size-independent criteria are NO and ALL exclusions are NO, output a single line:
"No size-independent criteria or exclusions apply."

If at least one criterion or exclusion is YES or UNKNOWN, show only those rows (omit all NO rows), followed by a compact paragraph explaining the impact on classification:

| Criterion | Applicable |
|---|---|
| [only rows that are YES or UNKNOWN] |

| Exclusion | Applicable |
|---|---|
| [only rows that are YES or UNKNOWN] |

[1-2 sentences explaining what each YES/UNKNOWN means for the classification. E.g.: "DNS service providers are in scope regardless of size and classified as essential (Article 3(1)(b)). CER Directive status could not be determined — if confirmed, the entity would also qualify as essential."]

If only criteria have YES/UNKNOWN rows but no exclusions (or vice versa), omit the empty table entirely.

### Missing Information
[List the 3-5 most important data points the user should provide or verify for a definitive assessment. Only include entity-specific data gaps (e.g., unverified employee count, missing turnover figure, unclear group structure). Do not include generic items that apply to every NIS-2 entity (e.g., "check national transposition law", "assess ICT/OT systems").]

### Data Sources & Assumptions

For each data point, cite the exact source. Permitted source labels are: the full URL that was fetched (e.g., "https://example.com/about-us"), "User input" (if the user provided the data), "Inferred" (e.g., for sector mapping), or "UNKNOWN". If the user provided a data point directly, always use "User input" as source. Never use vague labels like "Web search", "Web search results", or just site names without URLs.

| Data Point | Source | Confidence |
|---|---|---|
| Country | [full URL or User input] | HIGH / MEDIUM / LOW |
| Main activity | [full URL or User input] | HIGH / MEDIUM / LOW |
| Sector mapping | Inferred from activity → NACE mapping | HIGH / MEDIUM / LOW |
| Employee count | [full URL or User input or UNKNOWN] | HIGH / MEDIUM / LOW |
| Annual turnover | [full URL or User input or UNKNOWN] | HIGH / MEDIUM / LOW |
| Group structure | [full URL or User input or UNKNOWN] | HIGH / MEDIUM / LOW |

### Disclaimer

**Disclaimer:** This is an initial assessment based on the information provided and the EU NIS-2 Directive (2022/2555) as published. Member States transpose NIS-2 into national law with possible variations in scope, entity designation, and thresholds. This analysis provides an indicative EU-level assessment. For a legally binding determination, consult the applicable national transposition law and/or a qualified legal advisor. Information inferred from the company website may be incomplete or outdated.
```

