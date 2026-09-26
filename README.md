# Evaluating the Evaluators

Data and figure archive for a study of construct validity, representation
robustness, and semantic alignment in neural text-generation metrics.

This archive contains the observations and derived artifacts reported in the
article. It intentionally contains no source code, executable notebooks, web
interface, test suite, model weights, or launch configuration.

## Contents

- `data/generated/`: 220,800 unedited model-generated texts in six Parquet
  files, plus a file manifest;
- `data/source_index/`: source-dataset revisions, selected row indices, labels,
  and content hashes, without third-party source text;
- `results/conditional/`: metric, contrast, paired-difference, hypothesis, and
  equivalence tables for the conditional AG News experiment;
- `results/open_ended/`: metric, contrast, paired-difference, and hypothesis
  tables for the five-domain open-ended experiment;
- `results/canonical/`: publication-level synthesis tables, validation tables,
  and supplementary figures;
- `figures/article/`: the six figure PDFs supplied with the article;


The most direct entry points are:

- `results/canonical/tables/h1_h4_synthesis.csv` for the four confirmatory
  conclusions;
- `results/canonical/tables/construct-validity.csv` for V1;
- `results/canonical/tables/encoder-pair-correlations.csv` and
  `encoder-panel-stability.csv` for V2;
- `results/canonical/tables/cluster-semantic-validity.csv` for V3;
- `figures/article/FIGURE_SOURCES.csv` for the mapping between article figures
  and underlying tables.
