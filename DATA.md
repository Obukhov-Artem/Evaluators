# Data

## Generated texts

`data/generated/` contains all 220,800 model outputs used in the two completed
protocols. The original 2,208 run partitions were consolidated without changing
row values.

| File | Protocol and domain | Rows | Original partitions |
| --- | --- | ---: | ---: |
| `conditional.parquet` | conditional / AG News | 76,800 | 768 |
| `open_ag_news.parquet` | open-ended / AG News | 28,800 | 288 |
| `open_amazon_reviews.parquet` | open-ended / Amazon reviews | 28,800 | 288 |
| `open_dbpedia.parquet` | open-ended / DBpedia | 28,800 | 288 |
| `open_imdb_reviews.parquet` | open-ended / IMDb reviews | 28,800 | 288 |
| `open_yahoo_answers.parquet` | open-ended / Yahoo Answers | 28,800 | 288 |

The Parquet columns are:

| Column | Meaning |
| --- | --- |
| `sample_id` | immutable sample identifier |
| `run_id` | generation-cell identifier |
| `study_id` | study identifier |
| `condition_id` | fingerprint of the experimental condition |
| `prompt_id` | prompt-template identifier |
| `requested_label` | requested AG News label; null for open-ended generation |
| `prompt_text` | rendered generation prompt |
| `raw_output` | decoded model output |
| `normalized_output` | normalized output used downstream |
| `model_id` | generator alias from the study specification |
| `model_revision` | pinned base-model revision |
| `sampling_seed` | per-sample deterministic seed |
| `generated_at` | recorded UTC generation time |
| `metadata_json` | factor levels, token counts, batch seed, and runtime diagnostics |

`data/generated/manifest.csv` records row counts, source-partition counts, and
SHA-256 hashes. Sample identifiers are unique across all 220,800 rows.

## Source datasets

Third-party source text is not included. The file
`data/source_index/source_datasets.csv` records the provider, repository, exact
revision, split, row count, snapshot identifier, and content fingerprint for
eight dataset snapshots.

`data/source_index/source_dataset_index.parquet` contains 23,998 selected-row
records with provenance, labels, source indices, row hashes, and text hashes. It
contains no `text`, `title`, or `content` column. The index can be used to fetch
the named upstream revision, select the recorded rows, and verify their hashes.

The upstream datasets are:

- `fancyzhx/ag_news` at `eb185aade064a813bc0b7f42de02595523103ca4`;
- `fancyzhx/dbpedia_14` at `9abd46cf7fc8b4c64290f26993c540b92aa145ac`;
- `mteb/yahoo_answers_topics` at `c4d89f9633025d50954ab98a4c2c2feb188f6279`;
- `mteb/amazon_polarity` at `ec149c1fe36043668a50804214d4597804001f6f`;
- `stanfordnlp/imdb` at `e6281661ce1c48d982bc483cf8a173c1bbeb5d31`.

## Numerical results

The `results/conditional/data/` and `results/open_ended/data/` directories hold
complete Parquet tables. Their neighboring `tables/` directories contain CSV
renderings for direct inspection.

Equivalence testing was specified only for H3 in the conditional protocol. The
open-ended evidence bundle contained empty equivalence placeholders; those
zero-row, zero-column files are not included in this archive. The conditional
bundle likewise contained an empty rank-stability CSV placeholder because that
analysis belonged to the open-ended protocol; it is also omitted.

`results/canonical/data/full-metrics.parquet` is the compact validation metric
table. The canonical CSV files preserve construct-validity responses,
encoder-pair correlations, cluster-semantic diagnostics, and the H1--H4
publication synthesis.
