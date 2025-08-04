# Bioinformatics---Functional-and-compositional-relationship-between-myosin-proteins
Bioinformatics: Functional and compositional analysis of muscle-related gene clusters in C. elegans, with focus on myosins, GO enrichment and feature distribution.

# 🧬 Bioinformatics: Functional & Compositional Analysis of Muscle-Related Gene Clusters in *C. elegans*

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License: CC BY 4.0](https://licensebuttons.net/l/by/4.0/88x31.png)
![Platform](https://img.shields.io/badge/Platform-Jupyter%20%7C%20Python-lightgrey)

> Comprehensive functional and compositional analysis of gene clusters related to muscle proteins in *Caenorhabditis elegans*, focusing on **myosins**, **Gene Ontology (GO) enrichment**, and gene **feature distribution**.

---

## 🧠 Project Overview

This repository presents an analysis pipeline for exploring muscle-related gene clusters in *C. elegans*, with emphasis on:

- Identifying clusters containing or excluding **myosin-related genes**.
- Performing **GO enrichment analysis** on non-myosin clusters.
- Characterizing gene feature distribution within clusters.
- Exporting detailed cluster data and summary statistics for downstream interpretation.

---

## 📂 Repository Structure

.
├── data/
│ ├── resdf3.xlsx # Summary of cluster data and annotations
│ └── other_data.pkl # Main gene annotation dataset
├── scripts/
│ ├── cluster_analysis.py # Scripts for filtering and annotation
│ └── go_enrichment.py # Scripts for GO enrichment using gprofiler
├── outputs/
│ ├── pixel_<peptide>_<start>.xlsx # Per-cluster detailed gene info
│ └── resdf.xlsx # Summary file with cluster metadata
├── LICENSE # Creative Commons license file
├── README.md
└── requirements.txt


---

## 🛠️ Features & Capabilities

- Identification and classification of gene clusters by myosin content.
- Filtering and exclusion of non-informative or myosin-related genes.
- GO enrichment analysis via [gprofiler](https://biit.cs.ut.ee/gprofiler/gost).
- Automated export of cluster-level data to Excel files.
- Generation of summary tables capturing cluster composition and features.

---

## 🧪 Methods & Workflow

### 1. Gene Filtering & Cluster Grouping
- Target peptides (e.g., myosins like `MYO2_CAEEL`) are used to filter relevant entries.
- Genes are grouped by `Kclust` cluster IDs.
- Clusters are flagged based on presence/absence of myosin-related genes (using keywords like `myo-1`, `myo-3`, `unc-54`).

### 2. Gene Ontology (GO) Enrichment
- Clusters without myosin genes are subjected to GO enrichment analysis using `gprofiler`.
- Non-informative sources (e.g., transcription factors, miRNAs) are filtered out.

### 3. Output Generation
- Cluster gene lists and annotation data are exported as Excel files for each peptide and start position.
- A summary Excel file (`resdf.xlsx`) compiles cluster metadata and myosin presence flags.

---

## 📊 Sample Output Preview

| Start | Kclust | Othermyos |
|-------|--------|------------|
| 125   | 4      | False      |
| 237   | 7      | True       |
| ...   | ...    | ...        |

- `Othermyos = False` indicates the cluster **does not contain myosin-related genes** and is prioritized for GO analysis.

---

## 💾 Analysis & Setup

### Prerequisites

- Python 3.8 or higher
- Required packages (listed in `requirements.txt`):
  - pandas
  - numpy
  - Matplotlib
  - Seaborn
  - gprofiler-official
  

### Analysis

```Anaconda- jupyter nootebook
# pickle cluster.ipynb

# 📌 Example notebook: Muscle-Related Gene Cluster Analysis in C. elegans

import pandas as pd
from gprofiler import GProfiler

# Load input data
df_pkl = pd.read_pickle("data/other_data.pkl")
summary_df = pd.read_excel("data/resdf3.xlsx")

# Initialize GProfiler
gp = GProfiler(return_dataframe=True)

# Filter clusters that do not contain myosin-related genes
no_myosin_clusters = summary_df[summary_df["Othermyos"] == False]["Kclust"].unique()

results_list = []

# Loop over non-myosin clusters and run GO enrichment
for kclust_id in no_myosin_clusters:
    subdf = df_pkl[df_pkl["Kclust"] == kclust_id]
    gene_list = list(subdf["Gene Names (primary)"].dropna().unique())

    if not gene_list:
        continue

    results = gp.profile(organism='celegans', query=gene_list, no_evidences=False)
    results = results[~results["source"].isin(["TF", "MIRNA", "HP"])]
    results["Kclust"] = kclust_id
    results["GeneList"] = ", ".join(gene_list)
    results_list.append(results)

# Combine all results
final_go_df = pd.concat(results_list)
final_go_df.to_excel("outputs/go_enrichment_results.xlsx", index=False)

print("✅ GO enrichment complete. Results saved.")
```



## 📚 References

C. elegans Genome Database: Uniprot.org

GProfiler tool: https://biit.cs.ut.ee/gprofiler/

Myosin gene annotations: Relevant literatures and UniProt


