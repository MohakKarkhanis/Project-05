# Project-05
Genome Wide Association Study (GWAS) on Rice Traits
GWAS is a technique wherein the genome of Rice is screened to identify SNPs associated with important traits. This particular technique looks for statistical correlations while comparing genetic makeup of individuals who have a particular trait with those which lack it. If the variant is found significantly more associated with that trait then it is considered to be a successful association. Widely used in agriculture mainly to identify and correct genetic defects in crops while maintaining its functionality (if beneficial for the Rice).

This repository contains the code, methodology, and results for a Genome-Wide Association Study (GWAS) where the [Steps_Followed.docx](Steps_Followed.docx) file provides a highly detailed, step-by-step walkthrough of the entire pipeline, including data mapping, quality control logic, shell commands, and R scripts for visualization. Due to the immense size of raw genomic data (bed, bim, fam files), only the processed results and analysis scripts are hosted here. 

**Tools**
1. Core GWAS software: PLINK 1.9
2. Data Processing: Python- Pandas, NumPy, Regex
3. Visualization and Annotation: R (`qqman`, `data.table`), Python (`Matplotlib`, `Seaborn`)

**Methodology**
1. Data Acquisition: Harvested the `3K RG morpho-agronomic` phenotype dataset and the `3K RG 1M GWAS SNP` genotype dataset ([bed](https://3kricegenome.s3.amazonaws.com/snpseek-dl/3k-pruned-v2.1/pruned_v2.1.bed), [bim](https://3kricegenome.s3.amazonaws.com/snpseek-dl/3k-pruned-v2.1/pruned_v2.1.bim), [fam](https://3kricegenome.s3.amazonaws.com/snpseek-dl/3k-pruned-v2.1/pruned_v2.1.fam) files) from the International Rice Research Institute (IRRI) SNP Seek Database.
2. Quality Control (QC) via PLINK: Applied a strict filtering pipeline to remove noise and false positives:
a. **SNP Missingness:** Removed SNPs missing in >10% of individuals using `--geno 0.1` command.
b. **Indivudal Missingness:** Removed individuals missing >10% of their genotype calls using `--mind 0.1` command.
c. **Minor Allele Frequency:** Removed rare variants with an allele frequency <1% (`--maf 0.01`)
d. **Filtering using Hardy-Weinberg Equilibrium:** Removed SNPs that significantly deviated from HWE as they denoted genotypic errors, population substructure or selection affecting the overall quality of data. `--hwe 0.001` revealed a Wahlund Effect (Population Stratification) due to different rice subspecies mixed in the dataset. This effect arises when the sample consists of individuals from two or more distinct subpopulations like different rice varieties in the same dataset. These subpopulations have different allele frequencies for many SNPs which leads to high deviation which mainly arises due to mixed genetic background rather than genotypic errors.
e. **Filtering by High Relatedness:** Identified and removed one individual from each pair of highly related individuals like parent-offspring, full siblings while still maintaining the threshold. Calculated pairwise Identity-By-Descent (IBD) to generate `.genome` file, removing highly related individuals `PI_HAT > 0.125`.
Some of the Quality Control Data can be seen in the folder [Quality Control](https://github.com/MohakKarkhanis/Project-05/tree/main/Quality%20Control%20Data).
4. Capturing Genetic Variation: Performed PCA on the remaining 3001 samples to capture the genetic variations. The resulting eigenvectors (PC1 to PC5) were extracted using Python to serve as covariates in the final Mixed Linear model -see folder [Covariates and Eigenvectors](https://github.com/MohakKarkhanis/Project-05/tree/main/Covariates%20and%20Eigenvectors).
5. 
