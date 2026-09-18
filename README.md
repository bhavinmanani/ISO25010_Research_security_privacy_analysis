# Agentic PR Quality Analysis — TraceSEC

Empirical analysis of **40,214 GitHub pull requests** (AIDev dataset) investigating how ISO/IEC 25010 quality characteristics appear in AI-agent vs. human pull requests, combined with an LLM-assisted EU cybersecurity law compliance pipeline and manual requirements mapping.

**Research Practical WS2025/26 · University of Koblenz (RGSE)**  
Supervisors: Duaa Elsofi, Marco Ehl, Prof. Dr. Jan Jürjens  
Grade achieved: **1.7 (German scale)**

---

## What this project covers

Three linked studies, each tackling a different layer of the same problem: *software development artifacts encode security and quality signals — can we trace them systematically?*

### Phase 1 — Pull Request Analysis (AIDev dataset)

Keyword-based extraction of all 31 ISO/IEC 25010:2023 sub-characteristics across 939,409 PRs (932,791 agentic, 6,618 human). Four research questions:

| RQ | Question | Key finding |
|----|----------|-------------|
| RQ1 | How often are quality attributes mentioned in agentic vs. human PRs? | Agentic PRs mention quality terms ~5–10× more frequently across all eight top-level characteristics. Top four: User Assistance, Compatibility, Security, Maintainability. |
| RQ2 | Which characteristics co-occur? | Strongest pairs: Compatibility–Interoperability, Security–Testability, Reliability–Maintainability. |
| RQ3 | What do human reviewers focus on in agentic PRs? | Human review comments cluster around Security, User Assistance, Testability, and Compatibility — reviewers act as a quality validation layer. |
| RQ4 | Does mentioning quality terms correlate with PR acceptance? | Counter-intuitive: PRs *with* ISO terms: 59.2% acceptance vs. PRs *without*: 78.0%. Likely explained by PR scope, not quality awareness hurting acceptance chances. |

**Limitation to be aware of:** extraction is keyword-based, not a validated NLP classifier. The word "testing" alone inflates Testability counts considerably. Results are exploratory.

---

### Phase 2 — EU Cybersecurity Law Compliance Analysis (VisiOn Project)

A reusable three-part prompt pipeline applied to 7 deliverables of the VisiOn EU H2020 privacy platform, assessed against four regulations using GPT-4 and Gemini 2.5-Flash:

| Regulation | Scope | Verdict (7 deliverables) |
|------------|-------|--------------------------|
| CRA (Regulation 2024/2847) | Products with digital elements | ✅ YES — 7/7 |
| CSA (Regulation 2019/881) | ICT products & certification | ✅ YES — 7/7 |
| NIS2 (Directive 2022/2555) | Critical sector operators | ✅ YES — 7/7 |
| DORA (Regulation 2022/2554) | Financial sector entities only | ❌ NO — 0/7 |

**Prompt meta-model** (reusable for any regulation):
1. `Applies_IF` — does the regulation apply? Return YES at ≥70% confidence from project context.
2. `Applies_WHERE` — which components or SDLC phases are in scope?
3. `Implementation_HOW` — what specific actions are needed, citing the article/annex point?

**Important caveat:** CRA, NIS2, and DORA post-date the VisiOn project (2015–2017). This is a retrospective analysis — *what would need to change if built today* — not a real compliance obligation assessment. LLM confidence thresholds are design choices, not calibrated ground truth. The DORA NO verdict (based on hard sector exclusion) is the most trustworthy result in the matrix.

---

### Phase 3 — Requirements Mapping (VisiOn Privacy Requirements)

Manual mapping of 8 VisiOn privacy requirements (IDs 44–51) against three standards simultaneously:

- **ISO/IEC 25010:2023** quality characteristics (with standard section references)
- **CRA Annex I, Section 1.3 points (a)–(k)** cybersecurity requirements
- **OWASP ASVS v5.0.0** verification controls (with control IDs)

Key pattern: 6 of 8 requirements map to Interaction Capability sub-characteristics (operability, self-descriptiveness, user assistance), and CRA point 1.3(j) — "provide security-related information" — appears in 5 of 8 mappings. Transparency and notification are the dominant compliance theme in this requirement set.

**Limitation:** single-analyst mapping with no inter-rater reliability testing. Results are cross-verified using AI tools but should be read as well-reasoned proposals, not validated ground truth.

---

## Repository structure

```
├── notebooks/
│   ├── Phase1_AIDev_Quality_Analysis.ipynb   # RQ1–RQ4 keyword extraction & charts
│   └── Phase2_Compliance_Pipeline.ipynb      # LLM prompt pipeline for law analysis
├── reports/
│   ├── Phase1_Report.pdf
│   ├── Phase2_Report.pdf
│   ├── Phase3_Report.pdf
│   └── TraceSEC_Consolidated_Report.pdf      # Full three-phase report
└── README.md
```

---

## Stack

Python · Jupyter · pandas · matplotlib · Hugging Face Datasets · GPT-4 · Gemini 2.5-Flash

---

## Standards and datasets referenced

- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) — Software product quality model
- [OWASP ASVS v5.0.0](https://owasp.org/www-project-application-security-verification-standard/)
- [CRA — Regulation (EU) 2024/2847](https://eur-lex.europa.eu/eli/reg/2024/2847/oj/eng)
- [NIS2 — Directive (EU) 2022/2555](https://eur-lex.europa.eu/eli/dir/2022/2555/oj/eng)
- [CSA — Regulation (EU) 2019/881](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=LEGISSUM:4398780)
- [DORA — Regulation (EU) 2022/2554](https://eur-lex.europa.eu/eli/reg/2022/2554/oj/eng)
- [AIDev Dataset — SAIL Research / MSR 2026 Mining Challenge](https://2026.msrconf.org/track/msr-2026-mining-challenge)
- [VisiOn Project — EU H2020, Grant No. 653642](https://cordis.europa.eu/project/id/653642)
