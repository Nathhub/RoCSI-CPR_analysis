# 🌊 AtlantECO RoCSI-CPR 18S eDNA Metabarcoding Report

## Overview

This repository contains the full bioinformatics workflow and analysis for the **RoCSI-CPR eDNA project**, part of the EU-funded AtlantECO project.  
It documents the processing of environmental DNA samples collected along the Continuous Plankton Recorder (CPR) transect, targeting the **18S rRNA V9 region** and the **COI** to characterize eukaryotic plankton diversity.

Analyses were performed in **R (v4.5)** using **DADA2**, **phyloseq**, and rendered via **Quarto**.

---

## 📁 Repository Structure

<pre> ```
AtlantECO-RoCSI-CPR-report/
│
├── RoCSI-CPR_analysis.qmd # Quarto analysis file
├── RoCSI-CPR_analysis.html # Rendered report (open in browser)
├── RoCSI-CPR_analysis_files/ # HTML dependencies (figures, scripts, etc.)
│
├── data/
│ └── 18S/
│ ├── seqtab_nochim.rds # Non-chimeric ASV table
│ ├── taxa.rds # Taxonomy table (MZG database)
│ ├── Coordinates_RoCSI_CPR.csv # Sample coordinates and metadata
│ └── (optional) ps_object.rds # Saved phyloseq object
│
├── figures/ # Generated plots
├── renv/ # R environment folder
├── renv.lock # Dependency lockfile for reproducibility
├── .gitignore # Files excluded from GitHub
└── README.md # You are here
``` </pre>
---

## 🔬 Bioinformatics Summary

**Sequencing platform:** Illumina MiSeq v2 (Paired-end 2 × 150 bp)  
**Target:** 18S rRNA V9 region (primers 1389F–1510R, ~121 bp amplicon)  
**Processing steps:**

1. **Adapter and primer trimming** using *Cutadapt* (`v5.2`)  
   - Parameters: `-e 0.15`, `--overlap 10`, `--pair-filter=both`, `--discard-untrimmed`
2. **Quality filtering and denoising** with *DADA2* (`v1.30+`)
   - `truncLen = c(130, 125)`, `maxEE = c(2, 3)`, `pool="pseudo"`
3. **Merging and chimera removal**
   - `mergePairs(minOverlap = 20)`, `removeBimeraDenovo(method="consensus")`
4. **Taxonomic assignment** with the **MZG (Microbial Eukaryote + General Microbes)** database.
5. **Downstream analysis and visualization** in *phyloseq* and *ggplot2*.

---
