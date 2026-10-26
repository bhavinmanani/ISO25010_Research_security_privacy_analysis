# Phase 3 — Requirements Mapping

Manual mapping of 8 VisiOn privacy requirements (IDs 44–51) simultaneously against three standards: ISO/IEC 25010:2023, CRA Annex I Section 1.3, and OWASP ASVS v5.0.0.

---

## Objective

Three parallel mapping tasks per requirement:

| Task | Standard | What was mapped |
|------|----------|-----------------|
| Task 1 | ISO/IEC 25010:2023 | Quality sub-characteristic + section reference + justification |
| Task 2 | CRA Annex I, Section 1.3 (a)–(k) | Applicable point(s) + reason + importance |
| Task 3 | OWASP ASVS v5.0.0 | Relevant control ID(s) + reason + importance |

---

## Requirements analyzed

All 8 requirements are from the VisiOn EU H2020 privacy platform. They span two types: functional (PR) and non-functional (NFR/Usability).

| ID | Type | Description |
|----|------|-------------|
| 44 | PR / Privacy Verification | Platform shall notify citizen if further information is required to verify privacy requirements |
| 45 | PR / Information Usage | Platform shall analyse infrastructure of socio-technical system whenever external actors are involved |
| 46 | PR / Information Control | Platform shall represent/capture obligations specified by domain experts and applicable law governing personal information transmission |
| 47 | PR / Privacy Verification | Platform shall analyse whether specified information transmission is compliant with related laws |
| 48 | NFR / Usability | Platform shall visually notify PA user if information transmission meets/does not meet privacy requirements or applicable laws |
| 49 | NFR / Usability | Platform shall provide PA users with an integrated interface for all their activities |
| 50 | NFR / Usability | Platform shall provide citizen users with a web-based interface for all their activities |
| 51 | NFR / Usability | Platform shall represent the PLA concerning citizen information as a summary of allowed/forbidden activities |

---

## Mapping results

### Task 1 — ISO/IEC 25010:2023

| Req ID | Quality Characteristic | Sub-characteristic (section) |
|--------|----------------------|------------------------------|
| 44 | Interaction Capability | User Assistance (3.4.7), Self-descriptiveness (3.4.8) |
| 45 | Functional Suitability, Compatibility | Functional Completeness (3.1.1), Interoperability (3.3.2) |
| 46 | Functional Suitability | Functional Completeness (3.1.1), Functional Appropriateness (3.1.3) |
| 47 | Functional Suitability | Functional Correctness (3.1.2) |
| 48 | Interaction Capability | Self-descriptiveness (3.4.8), Appropriateness Recognizability (3.4.1) |
| 49 | Interaction Capability | Operability (3.4.3), Appropriateness Recognizability (3.4.1) |
| 50 | Interaction Capability, Flexibility | Operability (3.4.3), Adaptability (3.8.1) |
| 51 | Interaction Capability | Self-descriptiveness (3.4.8) |

**Pattern:** 6 of 8 requirements map to Interaction Capability sub-characteristics — the dominant quality theme across VisiOn's privacy requirements is *how the system communicates with users*, not how it performs internally.

---

### Task 2 — CRA Annex I, Section 1.3

| Req ID | CRA Point(s) | Core obligation triggered |
|--------|-------------|--------------------------|
| 44 | (j) | Provide security-related information — notification as transparency |
| 45 | (h) | Minimize attack surface — external actor involvement expands exposure |
| 46 | (d), (j) | Integrity of obligations + monitoring/accountability |
| 47 | (c), (d) | Confidentiality and integrity of data in transit |
| 48 | (j) | Security-related information — visual compliance notifications |
| 49 | (b), (h) | Access control mechanisms + reduced attack surface via centralized interface |
| 50 | (h) | Attack surface reduction — web interface is highest-exposure entry point |
| 51 | (b), (j) | Access control definitions + monitoring against allowed/forbidden activity rules |

**Pattern:** CRA point **(j)** — *provide security-related information* — appears in 5 of 8 mappings. Transparency and user notification are the dominant CRA theme in this requirement set.

---

### Task 3 — OWASP ASVS v5.0.0

| Req ID | ASVS Control(s) | Area |
|--------|----------------|------|
| 44 | V14.1.1, V14.2.4 | Data protection and privacy requirements documentation |
| 45 | V13.1.1, V13.2.4 | External communications and API security |
| 46 | V14.2.4 | Privacy controls and legal rules verification |
| 47 | V14.2.4 | Privacy compliance verification in data processing |
| 48 | V16.5.1, V16.3.2 | Authorization failure messages without information leakage |
| 49 | V8.4.2 | Administrative interface security with multiple layers |
| 50 | V3.1.1 | Browser security baselines for web-facing interfaces |
| 51 | V8.1.1 | Function-level and data-specific access control documentation |

---

## Cross-standard pattern summary

| Theme | ISO 25010 | CRA | OWASP ASVS |
|-------|-----------|-----|-----------|
| User transparency / notification | Self-descriptiveness, User Assistance | (j) | V16.5.1, V14.2.4 |
| Access control | Operability, Appropriateness Recognizability | (b) | V8.1.1, V8.4.2 |
| Attack surface reduction | Interoperability, Functional Completeness | (h) | V13.1.1, V13.2.4 |
| Data integrity and compliance | Functional Correctness | (c), (d) | V14.2.4 |

The three standards converge on the same underlying engineering concerns — they approach them from different angles (quality vs. legal obligation vs. verification control), but the root requirements they respond to are the same.

---

## Methodology

1. Read each VisiOn requirement and identified the core engineering intent
2. Matched to the most specific applicable ISO/IEC 25010 sub-characteristic using standard section references
3. Identified the narrowest applicable CRA Annex I point(s) from the (a)–(k) list
4. Matched to OWASP ASVS v5.0.0 controls by verification area and requirement type
5. Documented justification and importance for each mapping decision
6. Cross-checked mappings using AI tools (GPT-4, Gemini 2.5-Flash)

---

## Limitation

Single-analyst mapping with no inter-rater reliability testing. Results are well-reasoned proposals cross-verified with AI tools, but have not been validated against an independent expert assessment. The ISO sub-characteristic section references are precise; the OWASP control selections involve judgment calls, particularly where a requirement touches multiple verification areas.

---

## Files

```
phase-3-requirements-mapping/
├── README.md                         ← this file
└── results/
    └── requirements_mapping.pdf      ← full mapping tables for all 8 requirements
```

---

## References

- [ISO/IEC 25010:2023](https://www.iso.org/standard/78176.html) — Software product quality model
- [CRA — Regulation (EU) 2024/2847, Annex I Section 1.3](https://eur-lex.europa.eu/eli/reg/2024/2847/oj/eng)
- [OWASP ASVS v5.0.0](https://owasp.org/www-project-application-security-verification-standard/)
- [VisiOn Project — EU H2020, Grant No. 653642](https://cordis.europa.eu/project/id/653642)
