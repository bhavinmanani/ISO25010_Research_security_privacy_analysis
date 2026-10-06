# Phase 1 — AIDev Pull Request Quality Analysis

Keyword-based analysis of **40,214 GitHub pull requests** from the AIDev dataset, investigating how ISO/IEC 25010:2023 quality characteristics are distributed across AI-agent-generated and human-generated pull requests.

---

## Research questions

| # | Question |
|---|----------|
| RQ1 | How frequently are ISO/IEC 25010 quality characteristics mentioned in agentic PRs compared to human PRs? |
| RQ2 | Which quality characteristics frequently co-occur within the same PR? |
| RQ3 | Which quality characteristics do human developers discuss most in agentic PRs? |
| RQ4 | Is there a correlation between mentioning quality characteristics and PR acceptance rate? |

---

## Dataset

- **Source:** [AIDev Dataset — MSR 2026 Mining Challenge](https://2026.msrconf.org/track/msr-2026-mining-challenge)
- **Total PRs analyzed:** 40,214
- **Agentic PRs:** 33,596
- **Human PRs:** 6,618
- **Quality standard mapped:** ISO/IEC 25010:2023 (31 sub-characteristics)

---

## Key findings

### RQ1 — Frequency comparison
Agentic PRs mention quality attributes **5–10× more frequently** than human PRs across all eight top-level characteristics. Top attributes in agentic PRs: User Assistance, Compatibility, Security, Maintainability.

![RQ1 Quality Mentions](results/quality_mentions.png)

### RQ2 — Co-occurrence
Quality attributes do not appear in isolation — they cluster. Strongest co-occurring pairs:
- Compatibility ↔ Interoperability
- Security ↔ Testability
- Reliability ↔ Maintainability

![Co-occurrence Heatmap](results/cooccurrence_heatmap.png)

### RQ3 — Human reviewer focus
When reviewing agentic PRs, human developers cluster their comments around **Security, User Assistance, Testability, and Compatibility** — acting as a quality validation layer on top of AI-generated contributions.

![Human Comments](results/human_comments.png)

### RQ4 — Acceptance rate
Counter-intuitive result: PRs **with** ISO quality terms have a **59.2%** acceptance rate vs. **78.0%** for PRs without.

| Condition | Acceptance Rate |
|-----------|----------------|
| PRs with ISO/IEC 25010 terms | 59.2% |
| PRs without ISO/IEC 25010 terms | 78.0% |

Most likely explanation: PRs that explicitly discuss quality are larger, more complex changes — complexity drives rejection, not quality awareness itself.

![Acceptance Rate](results/acceptance_rate.png)

---

## Methodology

1. Loaded AIDev dataset (PRs, commits, comments, metadata)
2. Built a keyword dictionary for all 31 ISO/IEC 25010:2023 sub-characteristics
3. Applied keyword matching across PR titles, descriptions, and comment bodies
4. Separated results by PR type (agentic vs. human) and comment author (human vs. bot)
5. Computed co-occurrence matrix (filtered to pairs with > 50 joint appearances)
6. Compared acceptance rates with/without quality term presence

### Limitation
Extraction is keyword-based, not a validated NLP classifier. Inflated counts are possible — for example, the word "test" or "testing" alone triggers Testability. Results are **exploratory**, not production-grade metrics.

---

## Files

```
phase-1-aidev-analysis/
├── README.md                         ← this file
├── notebooks/
│   └── analysis.ipynb                ← full analysis: loading → extraction → RQ1–RQ4 → charts
└── results/
    ├── quality_mentions.png          ← RQ1 bar chart
    ├── cooccurrence_heatmap.png      ← RQ2 heatmap
    ├── human_comments.png            ← RQ3 bar chart
    └── acceptance_rate.png           ← RQ4 bar chart
```

---

## Stack

Python · pandas · matplotlib · seaborn · Jupyter

---

## How to run

```bash
# From repo root
pip install -r requirements.txt
cd phase-1-aidev-analysis/notebooks
jupyter notebook analysis.ipynb
```

---

## Reference

ISO/IEC 25010:2023 — [Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE)](https://www.iso.org/standard/78176.html)
