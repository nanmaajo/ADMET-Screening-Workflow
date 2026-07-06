[README.md](https://github.com/user-attachments/files/29712985/README.md)
# In Silico Antidiabetic Analysis of *Azadirachta indica* (Neem)

Molecular docking and ADMET study of neem leaf phytoconstituents against diabetes-associated protein targets, carried out during a Summer Internship at **Zygene Biotechnologies Pvt. Ltd.**, Kochi (May–June 2026), under the guidance of Ms. Fathima Zahrana, Stella Maris College (Autonomous), Chennai.

## Overview
This project evaluates four *Azadirachta indica* (neem) phytoconstituents — **Neophytadiene, Gamma-Elemene, Phytol, and Methyl Palmitate** — for antidiabetic potential using molecular docking, active-site prediction, and ADMET profiling. Results are benchmarked against four established antidiabetic drugs: **Epalrestat, Sitagliptin, Metformin, and Pioglitazone**.

The study also included a molecular diagnostics component: genomic DNA extraction from neem leaves, quantification, and PCR-based validation, confirming the plant material used for phytochemical reference.

## Objectives
- Isolate genomic DNA from fresh *Azadirachta indica* leaf tissue via magnetic bead-based extraction, followed by NanoDrop quantification and PCR validation
- Evaluate the antidiabetic potential of neem phytoconstituents through structure-based CADD and ADMET profiling

## Protein Targets & Ligand Pairs

| PDB ID | Protein | Test Ligand (Neem) | Reference Drug |
|---|---|---|---|
| 1ADS | Human Aldose Reductase | Neophytadiene | Epalrestat |
| 1Q5K | Dipeptidyl Peptidase-IV (DPP-IV) | Gamma-Elemene | Sitagliptin |
| HNP | Human Neutrophil Peptide | Phytol | Metformin |
| 4K1L | 11β-Hydroxysteroid Dehydrogenase Type 1 | Methyl Palmitate | Pioglitazone |

## Workflow

**1. Genomic DNA Extraction & Validation**
- Magnetic bead-based extraction (Zymag™ Plant/Algae DNA Extraction Kit) from fresh neem leaves
- NanoDrop quantification: 114.35 ng/µL and 116.94 ng/µL (samples N1, N2)
- Agarose gel electrophoresis (1% for gDNA, 1.5% for PCR product) and PCR amplification (rbcL primers) confirmed DNA integrity and suitability for downstream analysis

**2. Target Protein Preparation**
- Structures retrieved from RCSB PDB, prepared in UCSF Chimera v1.18 (ligands/waters/heteroatoms removed, hydrogens added, energy minimized)
- Converted to PDBQT via AutoDock Tools

**3. Active-Site Prediction (CASTp 3.0)**

| Target | Pocket Area (Å²) | Volume (Å³) | Key Residues |
|---|---|---|---|
| 1ADS | 487.49 | 289.14 | Gly18, Thr19, Trp20, Tyr48 |
| 1Q5K | 531.33 | 619.96 | Ala170, His173, Arg209, Glu211, Asn213 |
| HNP | 228.33 | 228.29 | Lys5, Glu6 |
| 4K1L | 783.09 | 523.76 | Thr40, Gly41, Ser43, Lys44, Ile46, Asn119, Tyr183, Lys187 |

**4. Ligand Preparation**
- 3D structures retrieved from PubChem (SDF), converted to PDB via Open Babel

**5. Molecular Docking**
- AutoDock 4.2.6, Lamarckian Genetic Algorithm (population size 150, 2,500,000 energy evaluations, 10 runs per ligand)
- Ligands flexible (rotatable bonds); receptors rigid
- Lowest-energy pose selected per complex

**6. Visualization**
- 3D interactions: PyMOL 3.1.1 (stick ligands, cartoon/surface protein, dashed H-bonds)
- 2D interaction maps: LigPlot+ v2.3.1 (green dashed = H-bonds, red arcs = hydrophobic contacts)

**7. ADMET Profiling**
- SwissADME (Lipinski's Rule of Five, solubility class, GI absorption, BBB permeability)

## Tools & Databases Used
| Tool | Purpose |
|---|---|
| RCSB PDB | Protein structure retrieval |
| PubChem | Ligand structure retrieval |
| UCSF Chimera | Protein preparation |
| Open Babel | Ligand format conversion |
| CASTp 3.0 | Active-site prediction |
| AutoDock 4.2.6 / AutoDock Tools | Molecular docking |
| PyMOL 3.1.1 | 3D visualization |
| LigPlot+ v2.3.1 | 2D interaction diagrams |
| SwissADME | ADMET / drug-likeness prediction |

## Docking Results (Binding Energy, kcal/mol)

| Compound | Best Run | Binding Energy | H-Bonds | Key H-Bond Residues | Hydrophobic Contacts |
|---|---|---|---|---|---|
| Epalrestat (ref.) | 4 | −9.74 | 0 | None | 12 |
| Pioglitazone (ref.) | 4 | −9.09 | 4 | Asp245, Lys247, Glu6, Tyr271 | 7 |
| Neophytadiene | 3 | −7.05 | 5 | Asn272, Arg265, Ser263, Lys262, Val264 | 3 |
| Methyl Palmitate | 4 | −6.04 | 3 | Asn119, Ile46 | 13 |
| Gamma-Elemene | 6 | −5.44 | 0 | None | 10 |
| Sitagliptin (ref.) | 6 | −5.25 | 2 | Val155 | 7 |
| Metformin (ref.) | 6 | −4.36 | 2 | Asp245, Ile246 | 2 |
| Phytol | 8 | −4.16 | 1 | Lys5 | 11 |

**Key finding:** Neophytadiene was the strongest-binding neem compound overall (−7.05 kcal/mol, 5 H-bonds), outperforming its own reference drug pairing in H-bond count. Epalrestat and Pioglitazone remained the strongest binders overall among all eight compounds tested.

## ADMET Summary (SwissADME)

| Compound | MW (g/mol) | Solubility | GI Absorption | BBB Permeant | Lipinski Violations |
|---|---|---|---|---|---|
| Neophytadiene | 274.48 | Moderately soluble | Low | No | 1 (MLOGP > 4.15) |
| Phytol | 292.50 | Moderately soluble | High | No | 1 (MLOGP > 4.15) |
| Gamma-Elemene | 190.32 | Soluble | Low | No | 1 (MLOGP > 4.15) |
| Methyl Palmitate | 270.45 | Moderately soluble | High | Yes | 1 (MLOGP > 4.15) |
| Epalrestat | 196.22 | Soluble | High | No | 0 |
| Sitagliptin | 274.33 | Soluble | High | Yes | 0 |
| Metformin | 129.16 | Highly soluble | High | No | 0 |
| Pioglitazone | 261.38 | Moderately soluble | High | Yes | 0 |

All four neem phytoconstituents showed one Lipinski violation each (high lipophilicity, MLOGP > 4.15) but otherwise acceptable drug-likeness profiles.

## Discussion
Reference drugs generally formed more hydrogen bonds and showed stronger binding energies than the neem phytoconstituents, but the neem compounds consistently established multiple hydrophobic contacts within the same active-site pockets — indicating genuine, stable binding rather than weak/non-specific interaction. Neophytadiene in particular showed a binding profile competitive with reference-level compounds, making it the most promising lead candidate from this study.

## Conclusion
This internship combined molecular diagnostics (DNA-based plant authentication) with computational drug discovery (docking + ADMET) to evaluate *Azadirachta indica* as a source of antidiabetic lead compounds. All four tested phytoconstituents bound successfully to their respective diabetes-related targets via a mix of hydrogen bonding and hydrophobic interactions, with **Neophytadiene (−7.05 kcal/mol)** emerging as the most promising candidate. Findings support further **in vitro, in vivo, and clinical validation**.

## Repository Structure
```
├── dna_extraction/         # NanoDrop & gel electrophoresis results
├── protein_prep/           # Prepared receptor structures (1ADS, 1Q5K, HNP, 4K1L)
├── ligand_prep/            # Neem phytoconstituent structures
├── active_site_prediction/ # CASTp pocket analysis outputs
├── docking_results/        # AutoDock logs, binding poses, docking scores
├── visualization/          # PyMOL sessions + LigPlot+ 2D interaction diagrams
├── admet_analysis/         # SwissADME reports per compound
└── README.md
```

## Future Improvements
- Molecular dynamics simulations to assess binding stability of Neophytadiene–1ADS complex over time
- Expand screening to additional neem phytoconstituents (azadirachtin, nimbin, quercetin)
- In vitro enzyme inhibition assays to validate top computational hit
- Automate the docking/ADMET pipeline with Python scripting for batch screening

## Author
**Nanma Ajo**
M.Sc. Bioinformatics, Stella Maris College (Autonomous), Chennai
[LinkedIn](https://linkedin.com/in/nanma-ajo-ba669625b) | [GitHub](https://github.com/nanmaajo)

## References
Selected key references (full list available in the original report):
- Trott, O., & Olson, A. J. (2010). AutoDock Vina. *Journal of Computational Chemistry*, 31(2), 455–461.
- Daina, A., Michielin, O., & Zoete, V. (2017). SwissADME. *Scientific Reports*, 7, 42717.
- Tian, W., et al. (2018). CASTp 3.0. *Nucleic Acids Research*, 46(W1), W363–W367.
- Berman, H. M., et al. (2000). The Protein Data Bank. *Nucleic Acids Research*, 28(1), 235–242.
