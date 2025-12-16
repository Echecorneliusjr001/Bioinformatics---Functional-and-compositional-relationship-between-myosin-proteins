# Bioinformatics---Functional-and-compositional-relationship-between-myosin-proteins
Bioinformatics: Functional and compositional analysis of muscle-related gene clusters in C. elegans, with focus on myosins, GO enrichment and feature distribution.

# 🧬 Bioinformatics: Functional & Compositional Analysis of Muscle-Related Gene Clusters in *C. elegans*

# Functional and Compositional Analysis of Myosin Proteins

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![License](https://img.shields.io/badge/License-CC0--1.0-green.svg)
![Status](https://img.shields.io/badge/Project-Completed-success)
![Field](https://img.shields.io/badge/Field-Bioinformatics-orange)

Bioinformatics project investigating the **functional and compositional relationships between myosin proteins** in *Caenorhabditis elegans*.  
The work combines **amino-acid composition analysis, clustering, and functional enrichment** to complement traditional sequence-based approaches.

---

## 🧠 Project Overview

This repository contains scripts, notebooks, and outputs used to analyze muscle-related gene clusters in *C. elegans*, with a particular focus on **myosin isoforms (UNC-54, MYO-2)** and their compositional features.

Myosin proteins are highly conserved motor proteins, yet individual isoforms perform distinct mechanical and structural roles in muscle. While sequence homology explains part of this diversity, it does not fully capture isoform-specific behavior.

The analysis focuses primarily on **UNC-54** and **MYO-2** myosin isoforms in *C. elegans*.

The project explores how:
- Amino-acid composition contributes to protein function
- Compositional similarity complements homology
- Feature distributions relate to structural and functional specialization

---

## 📁 Repository Structure

├── data/ # Input datasets and processed summaries
├── scripts/ # Python scripts for clustering and enrichment
├── notebooks/ # Jupyter notebooks with analyses and plots
├── outputs/ # Excel files and generated results
├── figures/ # Figures used for interpretation/presentation
├── LICENSE # CC0-1.0 Universal
└── README.md # Project documentation


---

## 🚀 Key Features

- Identification of myosin-containing and non-myosin gene clusters  
- Gene Ontology (GO) enrichment analysis using **g:Profiler**  
- Amino-acid feature distribution profiling  
- Feature-based clustering and comparison across isoforms  
- Export of results to structured Excel files for downstream analysis  

---

## 🛠 Methodology

### 1. C-pos (compositional-positional) encoding & Gene Clustering
The workflow begins with segmentation of all annotated proteins from UniProt into overlapping 15-mer peptides, generating 2,425,165 million sequence windows suitable for uniform comparison. Each segment is encoded into a 19-dimensional C-Pos compositional vector, capturing amino-acid content and positional information. These vectors are grouped into ~20,000 clusters using K-means. Genes are grouped into clusters based on prior clustering outputs.  
Clusters are annotated by detecting known myosin genes (e.g. *unc-54*, *myo-2*).

### 2. Functional Enrichment
Clusters lacking myosin genes are subjected to GO enrichment analysis using the `gprofiler-official` Python package to uncover functional trends.

### 3. Compositional Analysis
Amino acids are categorized by chemical properties (charge, polarity, hydrophobicity, etc.), and feature distributions are compared across clusters and isoforms.

### 4. Output Generation
Results are saved as Excel files and figures suitable for reports, presentations, and further interpretation.

---

## Tools and Technologies

- **Python 3**
- **Jupyter Notebook**
- NumPy
- Pandas
- Matplotlib / Seaborn
- Scikit-learn
- STRING database (for interaction context)

---

## Key Findings

- Protein composition provides a complementary lens to sequence homology
- Overlapping compositional features indicate that homology alone cannot explain functional differences
- Distinct compositional profiles—particularly in rod-like and disordered regions—correlate with isoform-specific mechanical and structural roles
- Functional enrichment appears shaped by both homology and co-evolved compositional tuning

---

## 📦 Installation & Requirements

Clone the repository and install dependencies:


1. Clone the repository:
   ```bash
   git clone https://github.com/Echecorneliusjr001/Bioinformatics---Functional-and-compositional-relationship-between-myosin-proteins.git
2. Install dependencies
pip install -r requirements.txt
4. Launch Jupyter Notebook
Open the notebooks in the notebooks/ directory and run cells sequentially.

📊 Outputs

Typical outputs include:

annotated_gene_clusters.xlsx

go_enrichment_results.xlsx

Feature distribution plots

Cluster-level summaries

All outputs are stored in the outputs/ directory.

📚 License

This project is released under the CC0-1.0 Universal License, allowing unrestricted reuse, modification, and distribution.

📌 Notes

This repository accompanies a master’s thesis focused on protein composition as a predictor of biological function, demonstrating how compositional analysis adds value beyond sequence homology alone.
Citation

If you use or build upon this work, please cite the following study, which inspired the compositional analysis framework:

Atsarina, L.A., Torbjörn, N.O., Maja, J., Maria-Jose, G.B., Sally, P.W., Bokarewa, M.I., Mezzasalma, S.A. & Katona, G. (2024).
Deciphering peptide–protein interactions via composition-based prediction: a case study with survivin/BIRC5.
Machine Learning Science & Technology, 5, 025081.

✉️ Contact

For questions or collaboration inquiries, feel free to reach out via GitHub.



