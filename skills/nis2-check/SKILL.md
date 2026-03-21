---
name: nis2-check
description: "Perform a NIS-2 Directive applicability assessment for any EU-based or EU-operating entity. Use this skill whenever a user asks about NIS-2 applicability, NIS-2 compliance scope, whether a company falls under NIS-2, NIS-2 Betroffenheitsprüfung, or NIS-2 affected entities. Also trigger when the user mentions 'NIS2', 'NIS-2', 'NIS 2', 'Network and Information Security Directive', or asks whether an entity is an essential or important entity under EU cybersecurity law. The skill works by analysing a company's website (impressum, about page) to infer sector, activity type and size, then cross-referencing against the directive's scope rules. The user may also provide details directly (main activity, employee count, turnover, balance sheet total). All output is in English."
license: "Proprietary. See LICENSE.txt for complete terms."
---

# NIS-2 Applicability Check

This skill assesses whether a given entity falls within the scope of EU Directive 2022/2555 (NIS-2) and, if so, classifies it as an **essential** or **important** entity.

## Reference Data

Before performing any assessment, read the compressed NIS-2 criteria:
→ `references/nis2-criteria.md`

This file contains the authoritative scope rules, sector lists (Annex I + II), size thresholds, exceptions, and the decision flowchart you must follow.

---

## Workflow

### Step 1 — Gather Entity Information

The user provides **at minimum** one of:
- A company website URL
- A company name + country

They may **optionally** provide:
- Main business activity / sector
- Number of employees
- Annual turnover (€)
- Annual balance sheet total (€)

**If a website URL is given**, fetch the following pages (try common paths, adapt to the site's language and structure):

1. **Impressum / Legal notice / Imprint** — for the registered company name, legal form, registered address, and sometimes registry numbers
2. **About us / Über uns / Company / Who we are** — for business description, activities, products/services, employee count, group structure
3. **Homepage** — for high-level description of what the entity does

Use `web_fetch` on the provided URL first, then try appending common paths like `/impressum`, `/imprint`, `/legal-notice`, `/about`, `/about-us`, `/company`, `/ueber-uns`, `/unternehmen`, `/kontakt` to discover more information. Not every path will work — that is fine, just use what you find. Do not try more than 6-8 page fetches total to keep things efficient.

**Extract or infer the following data points:**

| Data Point | Source Priority |
|---|---|
| Legal entity name | Impressum > About page |
| Country of establishment | Impressum (registered address) |
| Main business activity | About page / homepage (infer from products, services, self-description) |
| Sector & subsector mapping | Infer from activity → match to Annex I / Annex II categories |
| Employee count | About page (often mentioned as "X employees" / "team of X" / "Xmitarbeiter") — if not found, mark as UNKNOWN |
| Turnover / Balance sheet | Rarely on websites — mark as UNKNOWN unless user provides or site states |
| Group membership | Check if entity mentions a parent company or group — relevant for size calculation |

**Important inference rules:**
- Be transparent about what is inferred vs. what is stated. Always label assumptions clearly.
- When the main activity could map to multiple sectors, list all plausible mappings and note the ambiguity.
- If employee count is not findable, explain that the user needs to provide it for a definitive size assessment, but still proceed with the sector analysis.
- If the entity appears to be a subsidiary, note that the parent group's size may apply.

### Step 2 — Assess Scope Applicability

Follow the decision flowchart from `references/nis2-criteria.md` Section 7 strictly:

1. **Sector match**: Does the entity's main activity fall within any Annex I or Annex II sector? Map the activity to specific sector → subsector → entity type. Be precise — quote the matching entity type definition from the extract.

2. **Size-independent check**: Does Article 2(2)–(4) apply? Check whether the entity is:
   - A telecom network/service provider
   - A trust service provider
   - A TLD registry or DNS service provider
   - A domain name registration service provider
   - A sole provider of a critical service
   - A critical entity under the CER Directive
   - A central/regional government public administration entity
   
   If yes → in scope regardless of size.

3. **Size threshold check**: If not size-independent, does the entity meet the medium-sized enterprise threshold?
   - ≥ 50 employees, OR
   - Annual turnover > €10 million, OR
   - Annual balance sheet total > €10 million
   
   If unknown, clearly state what information is missing and provide conditional conclusions (e.g., "IF the entity has ≥50 employees, THEN…").

4. **Exclusion check**: Does any exclusion apply?
   - Predominantly national security / defence / law enforcement activities
   - Covered by DORA (financial sector entities under Regulation 2022/2554)
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

**IMPORTANT: Do NOT show the entity profile, data sources, applicability analysis, or assessment walkthrough in the chat. Process everything internally and only output the final report.**

## Output

```markdown
## NIS-2 Applicability Assessment

---

### NIS-2 Applicability: [Symbol] **[Classification]**

[1-2 sentences explaining what this classification means in practice:

- If ESSENTIAL (🔴): "This entity is classified as an essential entity under NIS-2. Full obligations apply, including stricter supervision (ex ante + ex post) and higher fines (up to €10M or 2% global turnover)."

- If IMPORTANT (🟡): "This entity is classified as an important entity under NIS-2. NIS-2 obligations apply with lighter supervision (ex post only) and lower fines (up to €7M or 1.4% global turnover)."

- If NOT IN SCOPE (🟢): "Based on the available information, this entity does not fall within the scope of the NIS-2 Directive."

- If CONDITIONAL (⚠️): "The classification depends on missing information. Provide the requested data for a definitive assessment."]

---

### Result

| Criterion | Result |
|---|---|
| In scope | YES / NO / CONDITIONAL |
| Classification | ESSENTIAL / IMPORTANT / UNDETERMINED |
| Sector | [Annex I/II sector → subsector → entity type] |
| Size threshold | [met / not met / unknown] |
| Confidence | HIGH / MEDIUM / LOW |

- [Sector match reasoning — 1 sentence]
- [Size assessment — 1 sentence]
- [Size-independent criteria — 1 sentence, only if applicable]
- [Exclusions — 1 sentence, only if relevant]
- [Missing information or open points — 1 sentence per item, only if applicable]
- [Recommendation / next step — 1 sentence, only if applicable]

---

This assessment is based on the EU NIS-2 Directive (2022/2555). Member States transpose NIS-2 into national law with possible variations. For a legally binding determination, consult qualified legal counsel.
```

### Output Rules

- Do NOT add entity profiles, data source lists, or applicability analysis sections.
- Do NOT show assessment logic, decision tree walkthrough, or internal reasoning in the output.
- Keep bullet points after the result table to max 1 sentence each.
- Only include bullet points that are relevant — omit empty or non-applicable items.
- Keep the output to: header, classification with explanation, result table, bullet points, and note.

---

## Edge Cases & Guidance

- **Multi-sector entities**: If an entity operates across multiple sectors (e.g., an energy company with a logistics arm), assess each activity separately. The entity is in scope if ANY of its activities triggers NIS-2.
- **Holding companies / Groups**: The parent company's size may pull a smaller subsidiary into scope. Conversely, Member States may consider independence of network/information systems.
- **Financial entities**: Check whether DORA (Regulation 2022/2554) applies. If it does, NIS-2 risk management and reporting obligations are replaced by DORA — but the entity remains in the NIS-2 cooperation framework.
- **Entities just below size thresholds**: Member States may designate smaller entities under Article 2(2)(b)-(e) special criteria. Flag this possibility.
- **Website does not reveal enough**: If the website provides insufficient information, state clearly what is missing and provide the analysis conditionally. Prompt the user to supply the missing data.
- **Non-EU entities operating in the EU**: They are in scope if they provide services within the EU. They must designate a representative in the EU.