# ADMET Screening Workflow — Lipinski's Rule of Five & Drug-Likeness Prediction

A structure-based ADMET (Absorption, Distribution, Metabolism, Excretion, Toxicity) screening workflow applied to *Azadirachta indica* (neem) phytoconstituents and reference antidiabetic drugs, using SwissADME. Built from real screening data generated during a Bioinformatics Internship at Zygene Biotechnologies.

## Overview
Poor ADMET properties are one of the leading causes of drug candidate failure in clinical trials. This project demonstrates an early-stage in silico screening pipeline that evaluates physicochemical properties, drug-likeness (Lipinski's Rule of Five), solubility class, and GI/BBB permeability for a small compound library — before committing to expensive downstream docking or wet-lab validation.

## Compound Library

**Test compounds** (neem phytoconstituents):
- Neophytadiene
- Phytol
- Gamma-Elemene
- Methyl Palmitate

**Reference compounds** (established antidiabetic drugs, used as benchmarks):
- Epalrestat
- Sitagliptin
- Metformin
- Pioglitazone

## Workflow

1. **Structure retrieval** — 3D/2D structures obtained from PubChem (SDF/SMILES)
2. **ADMET prediction** — structures submitted to [SwissADME](http://www.swissadme.ch)
3. **Property extraction** — molecular weight, solubility class, GI absorption, BBB permeability, Lipinski violations
4. **Drug-likeness filtering** — flag compounds violating Lipinski's Rule of Five
5. **Comparative analysis** — benchmark neem compounds against reference drugs with known clinical approval

## Results

| Compound | MW (g/mol) | Solubility Class | GI Absorption | BBB Permeant | Lipinski Violations |
|---|---|---|---|---|---|
| Neophytadiene | 274.48 | Moderately soluble | Low | No | 1 (MLOGP > 4.15) |
| Phytol | 292.50 | Moderately soluble | High | No | 1 (MLOGP > 4.15) |
| Gamma-Elemene | 190.32 | Soluble | Low | No | 1 (MLOGP > 4.15) |
| Methyl Palmitate | 270.45 | Moderately soluble | High | Yes | 1 (MLOGP > 4.15) |
| Epalrestat | 196.22 | Soluble | High | No | 0 |
| Sitagliptin | 274.33 | Soluble | High | Yes | 0 |
| Metformin | 129.16 | Highly soluble | High | No | 0 |
| Pioglitazone | 261.38 | Moderately soluble | High | Yes | 0 |

### Interpretation
- All four neem-derived compounds share the **same single Lipinski violation** — high lipophilicity (MLOGP > 4.15) — while all four reference drugs pass with zero violations. This is a consistent, explainable pattern rather than random noise, and is typical of plant-derived terpenoids/lipids versus synthesized small-molecule drugs.
- **GI absorption** splits the neem set in two: Phytol and Methyl Palmitate show high absorption (favorable), while Neophytadiene and Gamma-Elemene show low absorption (less favorable) — a useful early filter for prioritizing which compound to carry forward into docking.
- **Methyl Palmitate** is the only neem compound predicted to cross the blood-brain barrier, which is a relevant flag depending on the therapeutic target (generally undesirable for a peripheral antidiabetic target, unless CNS activity is intended).
- None of the compounds are automatically ruled out — a single Lipinski violation is a common and often tolerable exception, not an outright disqualifier — but the lipophilicity flag would guide follow-up SAR (structure-activity relationship) work if these were to be optimized further.

## Tools & Databases
| Tool | Purpose |
|---|---|
| PubChem | Compound structure retrieval |
| SwissADME | ADMET / physicochemical property prediction |
| Lipinski's Rule of Five | Oral bioavailability / drug-likeness filter |

## How to Reproduce
1. Retrieve compound SMILES/SDF from [PubChem](https://pubchem.ncbi.nlm.nih.gov/)
2. Paste SMILES into [SwissADME](http://www.swissadme.ch)
3. Record: Molecular Weight, Solubility (ESOL/SILICOS-IT), GI Absorption, BBB Permeant, Lipinski Rule violations
4. Tabulate results and flag any compound with >1 Lipinski violation for closer review

## Repository Structure
```
├── swissadme_reports/     # Raw SwissADME output per compound (screenshots/PDFs)
├── compound_structures/   # SMILES / SDF files for each compound
├── results_summary.csv    # Tabulated ADMET properties
└── README.md
```

## Future Improvements
- Extend the library with additional neem phytoconstituents (azadirachtin, nimbin, nimbolide, quercetin, β-sitosterol)
- Add toxicity prediction using ProTox-II or pkCSM alongside SwissADME
- Cross-reference with PAINS/Brenk medicinal chemistry alerts (also available in SwissADME)
- Automate batch queries via a script rather than manual SwissADME submissions

## Related Work
This ADMET screen was used as a pre-filter alongside molecular docking in [Molecular-Docking-Azadirachta-indica-Diabetes](https://github.com/nanmaajo/Molecular-Docking-Azadirachta-indica-Diabetes) — see that repo for target-specific binding affinity results.

## Author
**Nanma Ajo**
M.Sc. Bioinformatics, Stella Maris College (Autonomous), Chennai
[LinkedIn](https://linkedin.com/in/nanma-ajo-ba669625b) | [GitHub](https://github.com/nanmaajo)
