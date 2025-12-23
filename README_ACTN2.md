# Multi-Scale AI Analysis of ACTN2 Regulation and Protein Structure

## Goal
To investigate how noncoding DNA variation near the ACTN2 gene influences predicted regulatory activity, and to contextualize these regulatory effects using the predicted 3D protein structure of ACTN2.

**This project integrates:**

DeepSEA for regulatory prediction from DNA sequence

AlphaFold protein structure predictions for functional context

The central idea is that regulatory variation may affect when, where, or how much ACTN2 is expressed, even when the protein structure itself remains conserved.

## Biological Background: ACTN2

ACTN2 (α-actinin-2) encodes a structural cytoskeletal protein essential for sarcomere organization in muscle cells. Dysregulation or mutation of ACTN2 has been implicated in cardiomyopathies and muscle disorders.

Genomic location: Chromosome 1 (largest human chromosome)

Functional role: Actin cross-linking and structural integrity in muscle fibers

Genomic Data and Reference Assemblies

## The DeepSEA analysis used two RefSeq genomic accessions corresponding to regions near ACTN2:

NC_000001.11 – Primary reference assembly for human chromosome 1

NC_060925.1 – Alternate haplotype/assembly representing human genomic variation

RefSeq includes alternate assemblies because the human genome contains structural variation that cannot be captured by a single linear reference. Each FASTA entry was treated as an independent input by DeepSEA.

DeepSEA: Regulatory Prediction from DNA Sequence
Model Overview

## DeepSEA is a convolutional neural network trained on thousands of ENCODE experiments to predict regulatory activity directly from DNA sequence, including:

Transcription factor binding

Histone modifications

DNase I hypersensitivity (chromatin accessibility)

DeepSEA does not identify genes or retrieve sequences automatically. It predicts regulatory signals only for the sequences provided as input.

Results: Predicted DNase Accessibility Near ACTN2

Despite relatively small sequence differences between the two assemblies, DeepSEA predicted differences in DNase accessibility near ACTN2:

One sequence exhibited higher predicted DNase accessibility

The other exhibited lower predicted DNase accessibility

## Interpretation
DNase accessibility reflects chromatin openness:

High DNase signal → open chromatin → greater regulatory potential

Low DNase signal → compact chromatin → reduced accessibility

These results suggest that noncoding variation near ACTN2 may alter regulatory activity, even when protein-coding regions remain unchanged.

## Why DNase Accessibility Was Analyzed

DeepSEA outputs many regulatory signals by default because it was trained across diverse ENCODE assays. DNase accessibility was selected for interpretation because it:

Is directly interpretable as chromatin openness

Is widely used to assess regulatory potential

Provides a clear link between sequence variation and gene regulation

## AlphaFold: Protein Structure Context for ACTN2
**Rationale**

To contextualize regulatory predictions, the predicted 3D structure of the ACTN2 protein was examined using AlphaFold Protein Structure Database.

Regulatory variants identified by DeepSEA occur in noncoding regions and therefore are expected to influence gene expression, not protein folding. Protein structure analysis provides functional context for understanding why regulatory control of ACTN2 is biologically important.

## Structural Overview

The AlphaFold-predicted structure of human ACTN2 reveals a conserved, multi-domain architecture, including:

N-terminal actin-binding domain

Central rod domain composed of spectrin repeats

C-terminal EF-hand domains involved in calcium binding

Most structured domains are predicted with high confidence, while lower-confidence regions correspond to flexible or linker segments.

## Interpretation

The conserved predicted structure supports the interpretation that noncoding regulatory variation primarily affects ACTN2 expression timing or magnitude, rather than altering protein structure. Proper regulation of ACTN2 is therefore critical to maintaining normal muscle and cardiac function, even when the protein sequence itself is unchanged.

**Cross-Scale Integration**

This project links multiple biological scales using AI models:

DNA regulation → DeepSEA predictions from noncoding sequence

Gene expression potential → chromatin accessibility

Protein structure → AlphaFold-predicted domains

Together, these analyses demonstrate how AI models can be used to interpret biological systems from genome to protein, while respecting the boundaries between regulatory and structural effects.

## Limitations and Future Directions

**Limitations**

DeepSEA predictions are in silico and not experimental measurements

AlphaFold predicts static structure and does not capture protein dynamics

Regulatory predictions were not validated with expression data

**Future Work**

Integrate RNA-seq data to link regulatory predictions to expression levels

Analyze disease-associated noncoding variants near ACTN2

Extend interpretability analysis to additional regulatory models

## References

Zhou & Troyanskaya, Nature Methods / Nucleic Acids Research – DeepSEA

NCBI RefSeq and Gene Database – ACTN2

AlphaFold Protein Structure Database
