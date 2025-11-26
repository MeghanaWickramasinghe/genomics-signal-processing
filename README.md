# Promoter Detection & Statistical Alignment

Promoters are short regulatory DNA motifs found upstream of genes and play a crucial role in transcription initiation.
This project implements an automated pipeline to detect promoter-like regions in bacterial genomes using pattern scanning, statistical motif modeling, and cross-genomic validation.

## 🔬 Project Overview

This repository contains the full implementation of:

- Extraction of upstream genomic regions  
- Detection of **WAWWWT** promoter-like 6-mers  
- Construction of a **Position Probability Matrix (PPM)**  
- Log-likelihood statistical alignment of promoter motifs  
- Cross-validation using multiple bacterial genomes  

The pipeline was initially applied to genome **GCA 900475505.1** and validated across several additional genomes.

---

## 🧬 Methodology Summary
### 1. Upstream Region Extraction

Extracted DNA segments from **–15 to –5 bp** upstream of each gene.


### 2. Promoter Pattern Detection

Scanned the first 100 regions for sequences matching:

`WAWWWT`  
`W = A or T (weak bases)`  
`2nd pos = A`  
`6th pos = T`  

These motifs are A/T-rich and biologically indicative of promoter regions.

### 4. Statistical Alignment

Sliding-window 6-mer scoring using:

$$
S = \sum_{i=1}^{6} \log(P_{b_i,i}) - S_{\text{consensus}}
$$

- Score ≥ consensus → promoter  
- Otherwise → non-promoter  


### 5. Cross-Genome Validation
Pipeline reapplied to genomes from students:
210079K, 210179R, 210504L, 210657G, 210732H.

---

## 📊 Key Results

### ✔ Promoter Detection (Assigned Genome)
- ~45% of sequences contained promoter-like motifs  
- **4.1%** exceeded statistical threshold (high-confidence promoters)  
- Score distribution shows clear separation between strong and weak motifs  

### ✔ Cross-Validation
Consistent detection rates across all tested genomes →  
**PPM generalizes well across bacterial species**, capturing a conserved A/T-rich promoter architecture.

### ✔ Repository Structure

```
├── data/
│   ├── genome_sequences/
│   ├── annotations/
│   └── upstream_regions/
│
├── analysis/
│   ├── ppm_construction.ipynb
│   ├── statistical_alignment.ipynb
│   └── cross_validation.ipynb
│
├── results/
│   ├── ppm_matrix.png
│   ├── consensus_logo.png
│   ├── alignment_score_distribution.png
│   ├── promoter_detection_summary.png
│   └── cross_validation_plot.png
│
└── README.md
```

## 🚀 How to Run the Pipeline
1. Install Dependencies
pip install biopython numpy matplotlib pandas

2. Run PPM Construction
python scripts/build_ppm.py

3. Run Statistical Alignment
python scripts/scan_upstream_regions.py

4. Run Cross-Genome Validation
python scripts/cross_validate.py

## 🧪 Tools & Technologies

Biopython – sequence processing & motif analysis

Python (NumPy, Matplotlib) – scoring, visualization

NCBI Datasets – genome & annotation retrieval


## 📚 References

Cock et al., Biopython, Bioinformatics (2009)

NCBI Datasets Documentation

Laurençon et al., NeurIPS 2024
