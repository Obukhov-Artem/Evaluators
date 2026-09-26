# Methodology

## Research questions

The study tested whether conclusions about compact language-model generators
remain stable when the evaluator representation changes and whether a
stability-based clustering rule improves on a feasible square-root baseline.

Four confirmatory hypotheses were specified:

1. H1: one-epoch QLoRA adaptation increases classifier-based Text Inception
   Score relative to prompt-only generation.
2. H2: within-corpus FBD generator rankings are more stable across encoders than
   reference-MAUVE rankings.
3. H3: QLoRA increases requested-label accuracy for the prespecified 1.5B and
   3B generators.
4. H4: stability-selected clustering exceeds the held-out stability of a
   feasible square-root cluster-count baseline.

## Shared design

Both protocols used six instruction-tuned generators: Qwen2.5-0.5B-Instruct,
SmolLM2-360M-Instruct, TinyLlama-1.1B-Chat-v1.0,
Qwen2.5-1.5B-Instruct, SmolLM2-1.7B-Instruct, and
Qwen2.5-3B-Instruct. Random seeds were 17, 29, 43, 59, 71, 83, 97, and 109.
Each generation cell contained 100 texts with at most 96 newly generated tokens.
The seed was the independent statistical unit.

## Conditional protocol

The conditional AG News protocol crossed six generators, prompt-only versus
QLoRA adaptation, temperatures 0.3 and 0.8, four requested labels, eight seeds,
and 100 texts per cell, producing 76,800 texts.

QLoRA used rank 16, alpha 32, dropout 0.05, NF4 four-bit quantization, double
quantization, and bfloat16 computation. Adapters were trained for one epoch on a
3,000-row stratified AG News snapshot. Independent DistilBERT and RoBERTa
classifiers were trained on a separate 3,000-row snapshot. The reference sample
contained 2,999 AG News test rows after exclusion of one exact duplicate.

Primary metrics were requested-label accuracy and Text-IS. Secondary metrics
included FBD, reference MAUVE, Distinct-2, valid-text rate, uniqueness,
empty-output rate, stopping diagnostics, and generated-token count.

## Open-ended protocol

The open-ended protocol crossed six generators, five domains, temperatures 0.3,
0.6, and 0.9, top-p values 0.8 and 0.95, eight seeds, and 100 texts per cell,
producing 144,000 texts. The domains were AG News, DBpedia, Yahoo Answers,
Amazon reviews, and IMDb reviews.

FBD and reference MAUVE were evaluated across the declared representation
models. Cluster analysis compared stability-selected k with a feasible
square-root rule and a dimension-derived candidate. Candidate values were 2, 4,
8, 12, and 16, with six repeated 80% subsamples used for selection.

## Statistical analysis

Confirmatory analyses used paired seed-level endpoints, 95% confidence
intervals, 2,000 bootstrap replicates, and exact sign-flip inference where the
number of pairs permitted it. The minimum number of pairs was eight.
Multiplicity was controlled within each study and across the publication H1--H4
family. H3 also had an equivalence analysis with margins -0.01 and 0.01 using a
90% confidence interval and two one-sided tests.

## Validation analyses

V1 measured metric responses to duplicate injection, cross-label contamination,
cross-corpus contamination, prefix truncation, and span shuffling.

V2 recomputed FBD and MAUVE rankings with MiniLM-L6-v2, MPNet-base-v2, and
BGE-small-en-v1.5. Pairwise Spearman correlation, Kendall tau-b, Kendall's W,
minimum pairwise agreement, and rank variance were evaluated over 30 complete
strata per seed.

V3 compared stability-selected, square-root, and dimension-derived partitions
on AG News, Yahoo Answers, and Amazon Polarity reference data. Measures included
resampling stability, silhouette, ARI, AMI, NMI, V-measure, homogeneity,
completeness, cluster-size balance, and degeneracy checks.
