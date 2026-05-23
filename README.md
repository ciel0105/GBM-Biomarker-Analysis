# GBM-Biomarker-Analysis
# In Silico Biomarker Discovery in Glioblastoma (GBM)

A computational pipeline for identifying and validating potential biomarkers in Glioblastoma Multiforme (GBM) using publicly available transcriptomic data from NCBI GEO.

---

## Objective

Glioblastoma Multiforme is the most aggressive primary brain tumor with a median survival of ~15 months. This project aims to identify differentially expressed genes (DEGs) in GBM versus normal brain tissue, understand their biological roles through pathway enrichment and network analysis, and validate candidate biomarkers using clinical survival data.

---

## Pipeline

```
NCBI GEO Database
       ↓
Differential Gene Expression Analysis (GEO2R)
adj. p-value < 0.05 | Upregulated: logFC > 1 | Downregulated: logFC < -1
       ↓
Pathway Enrichment Analysis (Enrichr)
Top 200 upregulated and downregulated genes
       ↓
Protein-Protein Interaction Network (STRING DB)
High confidence score: 0.700
       ↓
Hub Gene Identification
Most connected nodes in PPI network
       ↓
Survival Analysis (GEPIA2)
TCGA-GBM dataset | Overall Survival | Median cutoff
```

---

## Tools Used

| Tool | Purpose |
|---|---|
| NCBI GEO | Transcriptomic dataset source |
| GEO2R | Differential gene expression analysis |
| Microsoft Excel | DEG filtering and sorting |
| Enrichr | Pathway enrichment analysis |
| STRING DB | Protein-protein interaction network |
| GEPIA2 | Survival validation using TCGA-GBM |

---

## Key Findings

### Upregulated Genes — Top Pathways
Consistent across Reactome, KEGG, WikiPathways, MSigDB, BioCarta and more:

| Pathway | Significance |
|---|---|
| Cell Cycle / G2-M Checkpoint | Most enriched across all databases |
| Extracellular Matrix Organization | ECM remodeling and invasion |
| Epithelial Mesenchymal Transition | Tumor invasion mechanism |
| E2F Targets | Transcriptional cell cycle drive |
| RB Tumor Suppressor Bypass | Checkpoint loss |
| p53 Signaling | Tumor suppressor dysregulation |
| FOXM1 Transcription Factor Network | Master GBM oncogenic regulator |
| Angiogenesis / VEGF Signaling | Tumor vascularization |

### Downregulated Genes — Top Pathways
| Pathway | Significance |
|---|---|
| GABA Receptor Signaling | Normal neuronal function lost |
| Synaptic Transmission | Brain cell identity lost |
| Calcium Signaling (CAMK2B) | Neuronal signaling silenced |
| Neuron Differentiation | Dedifferentiation of tumor cells |
| Serotonin / Acetylcholine Receptors | Neurotransmitter pathways lost |

---

## PPI Network Results

### Upregulated Hub Genes
| Gene | Role |
|---|---|
| CDK1 | Master cell cycle kinase |
| TOP2A | DNA topoisomerase, mitosis |
| FOXM1 | Master transcription factor in GBM |
| MELK | Maternal embryonic kinase, GBM oncogene |
| PBK | PDZ-binding kinase, poor prognosis marker |
| RRM2 | Ribonucleotide reductase, DNA synthesis |
| NDC80 | Kinetochore complex, mitotic spindle |
| BIRC5 | Survivin, apoptosis inhibitor |
| CD44 | Invasion and cancer stem cell marker |
| EGFR | Epidermal growth factor receptor |

### Downregulated Hub Genes
| Gene | Role |
|---|---|
| GABRA1 | GABA-A receptor subunit |
| SYT1 | Synaptic vesicle transmission |
| CAMK2B | Calcium/calmodulin kinase |
| NEFL | Neurofilament light chain |
| NEUROD6 | Neuronal differentiation factor |
| HTR2A | Serotonin receptor |

### Network Statistics
- Nodes: 55 | Edges: 187
- Average degree: 6.8
- PPI enrichment p-value: < 1.0e-16
- Two functional modules identified: Cell Cycle/Proliferation and ECM/Invasion

---

## Survival Analysis Results (GEPIA2 — TCGA GBM)

### Upregulated Genes
| Gene | HR | p(HR) | Result |
|---|---|---|---|
| **CD44** | **1.4** | **0.048** | Significant |
| RRM2 | 1.4 | 0.071 | Trend |
| FOXM1 | 1.2 | 0.37 | NS |
| CDK1 | 0.88 | 0.47 | NS |
| EGFR | 1.0 | 0.90 | NS |
| MELK | 1.2 | 0.43 | NS |
| TOP2A | 0.84 | 0.34 | NS |
| NDC80 | 1.0 | 0.79 | NS |
| PBK | 1.1 | 0.48 | NS |
| BIRC5 | 0.86 | 0.41 | NS |

### Downregulated Genes
All downregulated hub genes showed uniform expression loss across GBM samples consistent with global neuronal dedifferentiation, precluding survival stratification.

---

## Drug Targets Identified

Upregulated hub genes are targetable by existing compounds (HMS LINCS KinomeScan):

| Drug | Target | Status |
|---|---|---|
| Palbociclib | CDK4/6 | FDA approved |
| Dinaciclib | Pan-CDK | Clinical trials |
| Seliciclib | CDK2/7/9 | Clinical trials |
| BI-2536 | PLK1 | Clinical trials |
| Gefitinib | EGFR | FDA approved |
| Sorafenib | Multikinase | FDA approved |

---

## Biological Summary

Upregulated genes in GBM converge on CDK1/FOXM1-driven cell cycle dysregulation with concurrent ECM remodeling and EMT activation — representing a hyperproliferative and invasive transcriptomic signature. CD44 emerged as the key independent prognostic biomarker (HR=1.4, p=0.048). Downregulated genes reflect complete silencing of normal neuronal function including GABA signaling, synaptic transmission and neuron differentiation — consistent with tumor dedifferentiation.

---

## Repository Structure

```
📦 GBM-Biomarker-Analysis
 ┣ 📂 upregulated_enrichr
 ┣ 📂 upregulated_String-db analysis
 ┣ 📂 upregulated_GEPIA2
 ┣ 📂 downregulated_enrichr
 ┣ 📂 downregulated_String
 ┣ 📂 downregulated_gepia2
 ┣ 📄 NCBI.xlsx
 ┣ 📄 upregulated_string_interactions.tsv
 ┣ 📄 upregulated_string_protein_annotations.tsv
 ┣ 📄 downregulated_string_interactions.tsv
 ┗ 📄 downregulated_string_protein_annotations.tsv
```

---

## How to Reproduce

All tools are free and web-based — no coding required:

1. **NCBI GEO** → search GBM dataset GSE4290 → GEO2R → define tumor vs normal groups → run analysis → download results
2. **Excel** → filter adj.p < 0.05 → sort by logFC → take top 200 up and downregulated genes
3. **Enrichr** (maayanlab.cloud/Enrichr) → paste gene list → analyze pathway enrichment
4. **STRING DB** (string-db.org) → multiple proteins → paste list → set confidence 0.700
5. **GEPIA2** (gepia2.cancer-pku.cn) → survival analysis → GBM dataset → plot per gene

---

## References

- Kuleshov MV et al. Enrichr. *Nucleic Acids Research*, 2016
- Szklarczyk D et al. STRING v11. *Nucleic Acids Research*, 2019
- Tang Z et al. GEPIA2. *Nucleic Acids Research*, 2019
- Barrett T et al. NCBI GEO. *Nucleic Acids Research*, 2013

---

## Author

Ujjawal Srivastava
Amity Institute of Biotechnology, Amity University
ujjawalsrivastava2006@gmail.com 
LinkedIn- www.linkedin.com/in/ujjawal-srivastava-b07128349

Independent academic project — In silico bioinformatics pipeline for GBM biomarker discovery.
