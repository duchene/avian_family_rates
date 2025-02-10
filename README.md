### Supplementary Information - Drivers of avian genomic change revealed by evolutionary rate decomposition

This repository contains the following files:

**Supp_Data_1_trait_data** - Descriptions of each of the trait variables considered including sources, and files including the raw trait and molecular rates data. For replicating the analyses in the study, it is advisable to use the data in the Supp_Data_2_data_sets_for_regression folder.

**Supp_Data_2_data_sets_for_regression** - csv data files as used in scripts for running regression and random forest analyses.

**Supp_Data_3_regression_results** - Coefficient estimates with uncertainty intervals for all regression analyses, and random forest importance for each analyses. Figures corresponding to each file are included.

**Supp_Data_4_enriched_pathways** - Results of enriched pathways, and relevant genes, for all principal components where any pathway was found as significantly over-represented. Results are shown in the form of pathview figures, with relevant genes in principal components highlighted in red.

**Supp_Data_5_scripts** - R scripts for all analyses, including rates decomposition, regressions, random forests, principal components, chromosome analyses, and gene over-representation tests.

**Supp_Data_6_RMSEs** - Root mean squared error diagnostics results for random forest analyses.

Large data files are available at the FigShare repository and include gene trees, species tree, ClockstaRX results, and chromosome analysis results.

To see results for rate decomposition (PCA) analyses, access the large data files and follow:

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

The code in this repository is usable under the GNU General Public Licence version 3.
