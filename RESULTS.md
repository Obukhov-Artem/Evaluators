# Results

## Confirmatory hypotheses

The publication family contains four prespecified tests. Three were supported after
publication-level multiplicity correction.

| ID | Result | Estimate | 95% CI | Raw p | Study-adjusted p | Publication-adjusted p |
| --- | --- | ---: | ---: | ---: | ---: | ---: |
| H1 | Supported | 0.011184 | [0.010084, 0.012177] | 0.003906 | 0.007812 | 0.015625 |
| H2 | Supported | 0.246526 | [0.231414, 0.261189] | 0.003906 | 0.003906 | 0.015625 |
| H3 | Not supported | 0.001250 | [-0.003320, 0.006798] | 0.343750 | 0.343750 | 0.343750 |
| H4 | Supported | 0.106834 | [0.101524, 0.112925] | 0.003906 | 0.003906 | 0.015625 |

H1 shows a small positive Text-IS change under one-epoch QLoRA. H2 shows a clear
advantage for FBD in cross-encoder model-ranking stability. H3 provides no evidence
for the prespecified one-sided improvement in requested-label accuracy for the 1.5B
and 3B models. Its 90% equivalence interval was [-0.002619, 0.006016], fully inside
the prespecified [-0.01, 0.01] bounds. H4 shows higher held-out stability for the
stability-selected clustering rule than for the feasible sqrt(n) rule.

The authoritative rows are in
`results/canonical/tables/h1_h4_synthesis.csv` and the study-level paired values are
under `results/conditional/` and `results/open_ended/`.

## Construct-validity checks

The V1 validation produced 45 metric-by-transformation trend tests. Twenty-six had
an adjusted p value below 0.05, but the response pattern was not universal:

- requested-label accuracy responded in the expected direction in all four
  applicable transformations;
- Text-IS had corrected evidence only for prefix truncation, not for duplicate
  injection or cross-label contamination;
- FBD had corrected evidence for cross-label contamination, duplicate injection,
  and prefix truncation, but not for cross-corpus contamination or span shuffling;
- reference MAUVE had corrected evidence for cross-label contamination and duplicate
  injection, but not for truncation, cross-corpus contamination, or span shuffling;
- valid-text rate was constant for all five transformations and therefore carried no
  severity information in this design.

This rules out the broad interpretation that any one score is a universal monotonic
indicator of every controlled degradation. Full slopes, confidence intervals, and
severity-level responses are in `construct-validity.csv` and
`degradation-responses.csv`.

## Encoder-panel stability

All 30 planned strata were complete for every seed. Across the eight seeds:

- mean pairwise Spearman correlation was 0.8611 for FBD and 0.6744 for MAUVE;
- the mean FBD-minus-MAUVE correlation advantage was 0.1868;
- FBD was more stable in 84.6% of strata on average;
- the mean Kendall tau-b advantage was 0.2090;
- no incomplete strata were recorded.

These findings extend H2 from the original two-encoder comparison to a three-encoder
panel. The seed summaries and all 1,440 encoder-pair correlations are included under
`results/canonical/tables/`.

## Cluster stability and semantic alignment

Across the three reference datasets, stability selection improved held-out stability
over sqrt(n) by 0.1378 on average. The gain varied strongly by dataset: 0.1703 for
AG News, 0.2084 for Amazon Polarity, and 0.0347 for Yahoo Answers.

Semantic agreement did not improve uniformly. The selected-minus-sqrt(n) AMI was
0.2200 for AG News, -0.0355 for Amazon Polarity, and -0.0180 for Yahoo Answers.
Silhouette values remained below 0.10 throughout the validation. The result supports
the stability endpoint in H4 but does not justify treating stability as a general
guarantee of semantically well-separated clusters.

## Supported and unsupported claims

Supported by the completed data:

- one-epoch QLoRA produced a small positive Text-IS change;
- FBD model rankings were more stable across the evaluated encoder panel than MAUVE
  rankings;
- stability-selected clustering improved held-out resampling stability relative to
  the feasible sqrt(n) baseline.

Not supported or contradicted:

- QLoRA did not improve requested-label accuracy for the prespecified 1.5B and 3B
  generators; the difference was practically equivalent to zero at the declared
  margins;
- no evaluated metric responded monotonically and significantly to every controlled
  degradation;
- better resampling stability did not imply uniformly better semantic label
  agreement or strong geometric separation.

## Scope of inference

The independent unit is the random seed, not the generated text. The experiments
cover six small English-language instruction models, five reference domains, the
declared decoding grid, and the pinned evaluator models. The validation modules are
exploratory and do not replace the confirmatory H1--H4 decisions.

