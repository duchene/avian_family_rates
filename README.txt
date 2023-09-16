### Supplementary materials - Avian family rates

This repository contains the following files:

**Supp_File_1_trait_data.xlsx** - Details on each of the trait variables considered including sources.

**Supp_File_2_enriched_pathways** - Results of enriched pathways, and relevant genes, for all principal components where any pathway was found as significantly over-represented. Results are shown in the form of pathview figures, with relevant genes in principal components highlighted in red.

**Supp_File_3_regression_data.Rdata** - Complete regression results in phylolm output format. See below for loading and visualising these results in R.

**regressions_data.csv** - Data table used for performing all phylogenetic regressions.

**0_run_crx.Rscript** - 

**1_basic_regressions.Rscript** - 

**2_pc_data.Rscript** - 

**3_per_chromosome.Rscript** - 

**4_plot_tree_w_data.Rscript** - 

You can download the gene trees, species tree, ClockstaRX results, and chromosome analysis results from the following link:
https://sid.erda.dk/cgi-sid/ls.py?share_id=hVS3naBtJ6 

In R, assuming that the *phylolm* package is installed, open and visualize regression results as follows:

```coffee
library(phyloml)
load('Supp_File_3_regression_data.Rdata')
lapply(multregs, summary)
```
