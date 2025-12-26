# Interpretable DNA ML Baseline: Promoter vs Non-Promoter Classification
## Overview

This project implements an interpretable machine learning baseline to distinguish promoter sequences from random genomic background DNA using short sequence statistics. The goal is to understand what signal is present in DNA sequences, how simple models learn it, and why deeper models (e.g. CNNs such as DeepSEA) are necessary for more complex regulatory reasoning.

**The pipeline follows a classic regulatory genomics workflow:**

FASTA sequences → k-mer features → logistic regression → evaluation (Accuracy, AUROC)

DNA consists of four nucleotides (A, C, G, T).
A 4-mer is any DNA string of length 4.

Total possible 4-mers: 4^4 = 256

- Each sequence is represented as a 256-dimensional vector

- Each dimension corresponds to the frequency of a specific 4-mer

**This converts biological sequences into numerical vectors:**

DNA → numbers → vectors → math

## Model

A logistic regression classifier is trained on these k-mer frequency vectors.

- One weight per 4-mer

- Linear, interpretable decision function

- Predicts a probability between 0 and 1 indicating how promoter-like a sequence is

This constrained model ensures that learned signal must be robust and biologically embedded, rather than memorized noise.

## Training Dynamics

- Training proceeds over 15 epochs, where each epoch is one full pass through the training data.

- Loss measures how far the model’s predicted probabilities are from the true labels (promoter vs non-promoter). Lower loss indicates better predictions.

<img width="1280" height="960" alt="loss_curve" src="https://github.com/user-attachments/assets/a4ce9558-19df-40b3-8dbc-bd216771b55d" />

Observed training loss:

epoch 1  →  loss = 0.655
epoch 15 →  loss = 0.398


**This decrease indicates that:**

- Model weights are being updated consistently

- Average prediction error is shrinking

- Separation between promoter and non-promoter sequences is improving

Conceptually, this represents learning in real time: a gradual reweighting of sequence patterns across epochs.

## Evaluation Results

Evaluation is performed on a held-out test set (unseen during training).

**Test Accuracy: 81.5%**

~8 out of 10 sequences correctly classified

**Test AUROC: 0.8879**

If one promoter and one non-promoter are chosen at random, how often does the model score the promoter higher?

An AUROC of 0.8879 means this occurs ~89% of the time.

**Importantly:**

- AUROC is threshold-independent

- Preferred in biology where class imbalance is common

- Measures ranking quality rather than binary decisions

## ROC Curve Interpretation

<img width="1280" height="960" alt="roc_curve" src="https://github.com/user-attachments/assets/a897eee2-dea9-4c2d-83ce-6d667b4b2fe0" />

- Positive class: promoter sequences

- Negative class: non-promoter background DNA

- True Positive Rate (TPR): fraction of real promoters correctly identified

- False Positive Rate (FPR): fraction of non-promoters incorrectly labeled as promoters

The ROC curve visualizes the tradeoff between sensitivity and false alarms as the decision threshold changes. A high AUROC indicates consistent separation between the two classes.

## Biological Interpretation: Motifs and Sequence Regularities

Promoters are known to be:

- Noncoding but regulatory

- Located near transcription start sites

- Enriched for transcription factor binding sites

Motifs are short DNA patterns (typically 6–10 bp) recognized by regulatory proteins.

While the model does not explicitly know motifs:

- Motifs are composed of overlapping k-mers

- The model learns fragments of motifs

- GC-rich k-mers are often weighted positively

- AT-rich k-mers are often weighted negatively

This demonstrates that:

Biological regulation creates statistical regularities in DNA that are learnable from sequence alone.

**What This Shows**

Promoter DNA is statistically distinct from background genomic DNA

- This distinction is detectable using short sequence patterns

- Simple linear models can capture part of this signal

- More complex structure (motif interactions, spacing, nonlinearity) motivates deeper models such as CNNs (e.g. DeepSEA)

This project serves as a baseline and interpretability foundation for regulatory genomics.

## Real-World Applications

**Baselines for Deep Learning**
Any CNN or transformer-based regulatory model must be compared against k-mer baselines to ensure it learns signal beyond simple sequence composition.

**Noncoding Variant Prioritization**
Variants that disrupt motif fragments or k-mer distributions may affect regulation, relevant to cancer, neurological disease, and rare variants.

**Interpretability and Sanity Checking**
The model provides transparent insight into which sequence patterns drive predictions, helping distinguish biological signal from artifacts.

## Conceptual Takeaway

Training corresponds to a gradual reshaping of a decision boundary in 256-dimensional feature space, separating promoter from non-promoter sequences. Loss curves track shrinking error over time, while AUROC quantifies how cleanly that separation emerges.

This project illustrates how structure in biology becomes computable, and how machine learning extracts that structure through incremental numerical updates.
