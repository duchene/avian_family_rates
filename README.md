### Supplementary materials - Avian family rates

This repository contains the following files:

**Supp_File_1_trait_data.xlsx** - Details on each of the trait variables considered including sources.

**Supp_File_2_enriched_pathways** - Results of enriched pathways, and relevant genes, for all principal components where any pathway was found as significantly over-represented. Results are shown in the form of pathview figures, with relevant genes in principal components highlighted in red.

**Supp_File_3_a-d** - Model-averaged regression data and results in phylolm and MuMIn formats. (a) and (b) correspond to trait data averaged across families, with analyses including (a), and excluding (b) palaeognaths, respectively. (c) and (d) are equivalent but for trait data belonging to the single species sampled for genomic data. Analyses for the former data (a and b) are reported in the study, since they represent more appropriately the molecular data (also demonstrated in their higher R-squared values). See further details below for loading and visualising these results in R.

**regressions_data_family.csv** and **regressions_data_species_traits.csv** - Data tables used for testing whether avian molecular rates at the family level are explained by life-history, morphological, habitat, and demographic traits.

**regressions_data_intergenic_regions.csv** and **regressions_data_coding_regions.csv** - Data tables for testing whether avian molecular rates across loci were explained by GC-content, gene lenght, and location of genes with respect to the ends of chromosomes. 

**0_run_crx.Rscript** - R script to run ClockstaRX usng the gene trees and species tree.

**1_2_lineage_regressions.Rscript** - R script to run regression analyses assessing the variables explaining lineage rates.

**1_2_locus_regressions.Rscript** - R script to run regression analyses assessing the variables explainign locus rates.

**2_pc_data.Rscript** - R script to extract data and perform enrichment analyses on principal components, and save basic figures. Analyses include extracting and plotting taxon contributions and correlations to principal components. Also included here are tests of chromosome over-representation at the ends of principal components.

**3_per_chromosome.Rscript** - R script to perform tests of overall chromosome rates.

**4_plot_tree_w_data.Rscript** - R scripts to make basic figures of rates and traits across lineages.

You can download the gene trees, species tree, ClockstaRX results, and chromosome analysis results from the following link:
https://sid.erda.dk/cgi-sid/ls.py?share_id=hVS3naBtJ6 

To open and visualize the reported lineage regression results, in R install the *MuMIn* and *phylolm* packages and type as follows:

```coffee
library(phylolm)
library(MuMIn)
load('Supp_File_3a_regression_data_family_traits.Rdata')

# Regressions are found in the multregs list, with one element for each regression.
# See list of dependent variables
names(multregsavg)

# See full results for each analysis
lapply(multregsavg, summary)
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

The code in this repository is usable under the GNU General Public Licence version 3.
