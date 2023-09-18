### Supplementary materials - Avian family rates

This repository contains the following files:

**Supp_File_1_trait_data.xlsx** - Details on each of the trait variables considered including sources.

**Supp_File_2_enriched_pathways** - Results of enriched pathways, and relevant genes, for all principal components where any pathway was found as significantly over-represented. Results are shown in the form of pathview figures, with relevant genes in principal components highlighted in red.

**Supp_File_3_regression_data.Rdata** - Complete regression results in phylolm output format. See below for loading and visualising these results in R.

**regressions_data.csv** - Data table used for performing all phylogenetic regressions.

**0_run_crx.Rscript** - R script to run ClockstaRX usng the gene trees and species tree.

**1_basic_regressions.Rscript** - R script to run all regression analyses.

**2_pc_data.Rscript** - R script to extract data and perform enrichment analyses on principal components, and save basic figures. Analyses include extracting and plotting taxon contributions and correlations to principal components. Also included here are tests of chromosome over-representation at the ends of principal components.

**3_per_chromosome.Rscript** - R script to perform tests of overall chromosome rates.

**4_plot_tree_w_data.Rscript** - R scripts to make basic figures of rates and traits across lineages.

You can download the gene trees, species tree, ClockstaRX results, and chromosome analysis results from the following link:
https://sid.erda.dk/cgi-sid/ls.py?share_id=hVS3naBtJ6 

To open and visualize regression results, in R install the *phylolm* package and type as follows:

```coffee
library(phylolm)
load('Supp_File_3_regression_data.Rdata')

# Regressions are found in the multregs list, with one element for each regression.
# See list of dependent variables
names(multregs)

# See full results for each analysis
lapply(multregs, summary)
```

To see results for rate decomposition (PCA) analyses:

```coffee
library(ClockstaRX)
load('alltrs.Rdata')
load('crx_dnds.Rscript')
sptr_unr <- unroot(sptr)

# All object names in PCA analysis (as per the prcomp function of the stats package)
ls(crxdnds$weighted.pca.clock.space$empPCA)

# Branch contributions per PC
rownames(crxdnds$weighted.pca.clock.space$empPCA$rotation)[which(sptr_unr$edge[,2] %in% 1:Ntip(sptr_unr))] <- sptr_unr$tip.label
((crxdnds$weighted.pca.clock.space$empPCA$rotation^2)*100)

# Branch loadings per PC
crxdnds$weighted.pca.clock.space$empPCA$rotation

# p-values per PC
crxdnds$weighted.pca.clock.space$pPCs

# p-values per branch per PC
rownames(crxdnds$weighted.pca.clock.space$pIL)[which(sptr_unr$edge[,2] %in% 1:Ntip(sptr_unr))] <- sptr_unr$tip.label
crxdnds$weighted.pca.clock.space$pIL

# See all branch ID (i.e., branch number with prefix V in PCA results matrices)
plot(sptr_unr)
edgelabels(bg = 'white')
```
