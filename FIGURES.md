# Figures

## Article figures

The directory `figures/article/` contains the six PDF figures supplied with the
article. `FIGURE_SOURCES.csv` gives their captions, roles, source tables, and
the relevant contrast or aggregation.

- Figure 1 is a conceptual overview of the study design.
- Figure 2 shows seed-level H1 Text-IS differences.
- Figure 3 shows seed-level H3 requested-label accuracy differences and the
  practical-equivalence region.
- Figure 4 compares mean pairwise encoder-rank correlations for FBD and
  reference MAUVE.
- Figure 5 is the controlled-degradation response matrix.
- Figure 6 compares changes in resampling stability and adjusted mutual
  information.

## Supplementary result figures

`results/canonical/figures/` contains six additional result views in both PDF
and PNG formats:

- `h1-h3-effects`;
- `h2-corpus-forest`;
- `construct-validity-forest`;
- `degradation-curves`;
- `encoder-stability-heatmap`;
- `cluster-stability-semantics`.

The PDF and PNG files are alternative renderings of the same underlying result
views. Numerical values should be taken from the CSV or Parquet tables rather
than digitized from a figure.
