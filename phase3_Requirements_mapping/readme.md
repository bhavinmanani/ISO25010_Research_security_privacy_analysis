# Phase 2 — LLM-Assisted EU Cybersecurity Law Compliance Analysis

A reusable three-part prompt pipeline that applies four EU cybersecurity regulations to 7 project deliverables of the VisiOn EU H2020 privacy platform using GPT-4 and Gemini 2.5-Flash.

---

## Research questions

| # | Question |
|---|----------|
| RQ2.1 | How can software quality engineering practices be operationalized for use with AI agents? |
| RQ2.2 | What meta-model for AI prompts improves compliance analysis based on international standards? |

---

## Regulations analyzed

| Regulation | Reference | Scope |
|------------|-----------|-------|
| Cyber Resilience Act (CRA) | Regulation (EU) 2024/2847 | Hardware & software products with network connectivity |
| EU Cybersecurity Act (CSA) | Regulation (EU) 2019/881 | ICT products, services, and certification |
| NIS2 Directive | Directive (EU) 2022/2555 | Essential and important entities in critical sectors |
| Digital Operational Resilience Act (DORA) | Regulation (EU) 2022/2554 | Financial sector entities only |

---

## Dataset

- **Project analyzed:** [VisiOn — EU H2020, Grant No. 653642](https://cordis.europa.eu/project/id/653642)
- **Deliverables assessed:** D1–D7 (privacy platform architecture, pilot deployments, dissemination reports)
- **LLMs used:** GPT-4, Gemini 2.5-Flash

> **Scope note:** VisiOn ran 2015–2017, predating CRA, NIS2, and DORA. This is a **retrospective analysis** — what compliance obligations would apply if the project were built today — not an assessment of actual legal obligations the project held.

---

## Prompt meta-model

The core contribution of this phase is a reusable three-part prompt structure applicable to any EU regulation:

```
Applies_IF    → Does this regulation apply to the artifact?
               Return YES if project-level context meets ≥70% confidence threshold.
               Return NO if a hard sector/scope exclusion applies.
               Return UNCLEAR only if context is genuinely insufficient.

Applies_WHERE → Which specific components, SDLC phases, or processes fall in scope?

Implementation_HOW → What concrete actions are required?
                     Cite the specific article and annex point from the regulation.
```

**Output format (JSON):**
```json
{
  "Applies_IF": "YES | NO | UNCLEAR",
  "Justification": "...",
  "Applies_WHERE": ["component or SDLC phase", "..."],
  "Implementation_HOW": ["action citing Article X", "..."]
}
```

Prompt files for each regulation are in the `/prompts` folder.

---

## Results

### Applicability matrix

| Regulation | D1 | D2 | D3 | D4 | D5 | D6 | D7 | Score |
|------------|----|----|----|----|----|----|-----|-------|
| CRA | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | 7/7 |
| CSA | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | 7/7 |
| NIS2 | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | 7/7 |
| DORA | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | 0/7 |

![Applicability Matrix](results/applicability_matrix.png)

### Key findings per regulation

**CRA** — All 7 deliverables inferred to involve network-connected components based on project context. Key obligations triggered: secure-by-default configurations, SBOM publication, vulnerability reporting within 24 hours.

**CSA** — Broadest applicability; certification pathways relevant for all pilot-deployed components (healthcare, public administration). Key obligations: user guidance for secure installation, security support duration declaration.

**NIS2** — Driven by the presence of health and public administration stakeholders (OPBG hospital, MISE ministry) named across deliverables. Key obligations: cybersecurity risk management framework, 24h/72h incident reporting to national CSIRT, cyber hygiene training.

**DORA** — Consistent NO across all 7 deliverables. VisiOn operates in health and government, not financial services — hard sector exclusion applies. The 0/7 result is the **most reliable finding in this analysis** because it is based on a hard exclusion rule, not probabilistic inference.

---

## Methodology

1. Summarized each regulation's scope, key articles, and software engineering obligations
2. Extracted three applicability dimensions per regulation (IF / WHERE / HOW)
3. Designed structured JSON-output prompts using the three-part meta-model
4. Applied prompts to each of the 7 VisiOn deliverables loaded as PDFs
5. Ran two prompt versions (literal vs. probabilistic inference) to test sensitivity
6. Synthesized results into per-law compliance tables

---

## Limitations

- **LLM confidence thresholds are design choices, not calibrated ground truth.** The 70% threshold for YES verdicts was set deliberately to eliminate UNCLEAR outputs — a different threshold would change results.
- **Probabilistic inference can over-attribute obligations.** D6 (a dissemination report) received YES under CRA, CSA, and NIS2 because the model inferred project context rather than evaluating the artifact itself. Future work should distinguish artifact-evidenced obligations from regulation-derived ones.
- **No ground truth validation.** Results were not cross-checked against a legal expert's independent assessment.
- **Retrospective analysis only.** These verdicts describe hypothetical compliance obligations, not legal findings about the VisiOn project.

---

## Files

```
phase-2-llm-compliance/
├── README.md                         ← this file
├── prompts/
│   ├── cra_prompt.txt                ← CRA compliance analysis prompt
│   ├── csa_prompt.txt                ← CSA compliance analysis prompt
│   ├── nis2_prompt.txt               ← NIS2 compliance analysis prompt
│   └── dora_prompt.txt               ← DORA compliance analysis prompt
└── results/
    └── applicability_matrix.png      ← 4×7 applicability heatmap
```

---

## Stack

Python · GPT-4 API · Gemini 2.5-Flash · PDF parsing · JSON output

---

## References

- [CRA — Regulation (EU) 2024/2847](https://eur-lex.europa.eu/eli/reg/2024/2847/oj/eng)
- [CSA — Regulation (EU) 2019/881](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=LEGISSUM:4398780)
- [NIS2 — Directive (EU) 2022/2555](https://eur-lex.europa.eu/eli/dir/2022/2555/oj/eng)
- [DORA — Regulation (EU) 2022/2554](https://eur-lex.europa.eu/eli/reg/2022/2554/oj/eng)
- [VisiOn Project — EU H2020, Grant No. 653642](https://cordis.europa.eu/project/id/653642)
