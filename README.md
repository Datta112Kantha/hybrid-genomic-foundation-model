# hybrid-genomic-foundation-model
Hybrid multi-scale DNA foundation model integrating motif-level (DNABERT-2) and long-range (HyenaDNA) representations for taxonomy and novelty detection across large genomic corpora. Manuscript in preparation for Bioinformatics (Oxford). Code will be released upon acceptance.

# Hybrid Multi-Scale DNA Foundation Model for Taxonomy and Novelty Detection

## Overview

This repository accompanies the research project:

**Hybrid Multi-Scale DNA Foundation Model for Taxonomy and Novelty Detection**  
*Manuscript in preparation for submission to* **Bioinformatics (Oxford Academic)**

The project introduces a multi-scale, evolution-aware genomic foundation model that unifies local sequence grammar, long-range genomic context, and phylogenetic structure within a single training framework. The model is designed to support taxonomic classification, novelty detection, and downstream genomic analysis across diverse microbial domains.

---

## Motivation

Existing genomic foundation models tend to specialize in one of three aspects:

- Short-range motif-level semantics (e.g., promoters, codon bias)
- Long-range genomic structure (kilobase-scale context)
- Evolutionary or taxonomic relationships

However, real biological sequences exhibit all three simultaneously. This work addresses that gap by introducing a hybrid architecture that jointly captures local sequence grammar and long-range structure, while explicitly incorporating evolutionary inductive bias during training.

---

## Model Architecture

The core contribution is a **hybrid multi-scale encoder**:

- **DNABERT-2** processes short sequences at 6-mer resolution to capture fine-grained motif-level semantics.
- **HyenaDNA**, tuned using **QLoRA**, models long-range genomic context with receptive fields up to 4 kb.
- Outputs from both pathways are projected into a **shared embedding space**, enabling unified downstream learning.

This design allows the model to reason jointly about gene-scale and genome-scale signals without retraining or re-tokenizing either backbone.

---

## Training Framework

The model is trained using a unified large-scale pipeline spanning eight genomic corpora:

- GTDB  
- IMG/VR  
- PLSDB  
- SILVA  
- MG-RAST  
- UBA MAGs  
- RefSeq  
- RefSeq Viral  

Key training features include:

- Deduplication across datasets to prevent information leakage  
- Biome-aware and source-balanced sampling  
- Semi-supervised learning using **phylogeny-informed MixMatch**  
- Multi-task objectives combining:
  - Masked Language Modeling (MLM)
  - Taxonomic classification
  - Novelty / out-of-distribution detection

---

## Evolutionary Inductive Bias

A central innovation of this work is the explicit incorporation of evolutionary structure into training:

- A **phylogenetic distance–aware loss** penalizes misclassification between distantly related taxa more heavily than between close relatives.
- Simple evolutionary augmentations (neutral substitutions, strand shifts) improve robustness to mutation and recombination.
- Learned embeddings reflect evolutionary distance rather than dataset-specific artifacts.

---

## Evaluation

The model is evaluated across diverse and challenging benchmarks, including:

- CAMI2 metagenomic challenges  
- simBac evolutionary simulations  
- Plasmid datasets  
- Ancient microbiome samples  
- IMG/VR dark virome sequences  

Performance is compared against strong baselines including **DNABERT-2**, **HyenaDNA**, **Kraken2**, and **Mash/ANI**. Predictions are validated using external biological tools such as **BLAST**, **GTDB-Tk**, **ANI**, and phylogenetic tree reconstruction, demonstrating accurate placement of unseen organisms and improved separation of distant taxa.

---

## Applications

This framework enables a range of downstream applications, including:

- Microbial taxonomic classification  
- Detection of previously unseen or divergent organisms  
- Pathogen surveillance and metagenomic analysis  
- Evolution-aware genomic representation learning  

---

## Repository Status

This repository is currently provided for **documentation and transparency purposes**.

To support a clean and reproducible release aligned with journal policies, the following are **not yet included**:

- Full training and inference code  
- Dataset preprocessing pipelines  
- Pretrained model weights  

---

## Code Availability

The full implementation will be released publicly **upon manuscript acceptance**.  
During peer review, the code can be made available to editors and reviewers upon request.

---

## Author

**Dattatreya Kantha**  
Washington, D.C., United States  
(On-site)

---


