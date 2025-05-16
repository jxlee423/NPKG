# NPKG (Network - Phenotype Integrated Key Gene screening)
This repository contains R package and example data for **NPKG: A novel approach for screening key genes
through integrated network and phenotype information.**

**NPKG is a machine learning approach incorporating gene network topology and phenotype-gene relationships to improve the key gene discovery
efficiency.**

![Overview](./docs/NPKGmodel.png)

## Required Packages
- WGCNA
- glmenet
- randomForest
- caret
- dplyr
- stats
- methods

We recommend using R version ≥ 4.4.2.

## Package Installation and Loading
You can install NPKG from GitHub with:
``` r
devtools::install_github("jxlee423/NPKG")
library(NPKG)
```

## Data Description
We provide the dataset derived from a study on Alzheimer’s disease at the Mount Sinai Medical Center Brain Bank (MSBB). After preprocessing, it contains 55 samples and 18434 genes.

NPKG needs two input dataset, and two necessary parameters:
gene_data: Preprocessed gene expression matrix (genes in columns, samples in rows)
pheno_data: Phenotype data frame containing sample information and traits.
pheno: Phenotype trait name.
pheno_group_fn: A function to classify phenotypes into "onset" and "non-onset" groups.

``` r
gene_data = pd.read_csv('../data/gene_data.csv')
pheno_data = pd.read_csv('../data/pheno_data.csv')
pheno = "CDR"
pheno_group_fn = function(x) ifelse(x >= 1, 1, 0)
NPKG(gene_data, pheno_data, pheno, pheno_group_fn)
```

## Optional Parameters of NPKG
- `p_threshold` : Module-trait correlation p-value threshold (default = 0.05).
- `gs_threshold` : Gene Significance threshold (default = 0.25).
- `mm_threshold` : Module Membership threshold (default = 0.75).
- `degree_top Hub` : genes degree threshold (default = 0.05).
- `clust_threshold` : Remove outlier samples through clustering (default = 0.95).
- `output_dir` : Output directory.
- `seed` : Random Seed.
- `verbose` : Whether to show progress messages.

## Output
The NPKG returns a list with the following components:

- `modules` : significantly phenotype-related modules.
- `final_genes` : Key genes in the final screen.

## Reference

1. Langfelder, P., Horvath, S. WGCNA: an R package for weighted correlation network analysis. BMC Bioinformatics 9, 559 (2008). https://doi.org/10.1186/1471-2105-9-559
