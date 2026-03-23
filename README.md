# Project-05
Genome Wide Association Study (GWAS) on Rice Traits
GWAS is a technique wherein the genome of Rice is screened to identify SNPs associated with important traits. This particular technique looks for statistical correlations while comparing genetic makeup of individuals who have a particular trait with those which lack it. If the variant is found significantly more associated with that trait then it is considered to be a successful association. Widely used in agriculture mainly to identify and correct genetic defects in crops while maintaining its functionality (if beneficial for the Rice).

This repository contains the code, methodology, and results for a Genome-Wide Association Study (GWAS) where the [Steps_Followed.docx](Steps_Followed.docx) file provides a highly detailed, step-by-step walkthrough of the entire pipeline, including data mapping, quality control logic, shell commands, and R scripts for visualization. Due to the immense size of raw genomic data (bed, bim, fam files), only the processed results and analysis scripts are hosted here. 

**Tools**
1. Core GWAS software: PLINK 1.9
2. Data Processing: Python- Pandas, NumPy, Regex
3. Visualization and Annotation: R (`qqman`, `data.table`), Python (`Matplotlib`, `Seaborn`)

**Methodology**
1. Data Acquisition: Harvested the [`3K RG morpho-agronomic`](https://s3-ap-southeast-1.amazonaws.com/oryzasnp-atcg-irri-org/3kRG-phenotypes/3kRG_PhenotypeData_v20170411.xlsx) phenotype dataset and the `3K RG 1M GWAS SNP` genotype dataset ([bed](https://3kricegenome.s3.amazonaws.com/snpseek-dl/3k-pruned-v2.1/pruned_v2.1.bed), [bim](https://3kricegenome.s3.amazonaws.com/snpseek-dl/3k-pruned-v2.1/pruned_v2.1.bim), [fam](https://3kricegenome.s3.amazonaws.com/snpseek-dl/3k-pruned-v2.1/pruned_v2.1.fam) files) from the International Rice Research Institute (IRRI) SNP Seek Database.
