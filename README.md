# PRS-PGx-TL
A transfer learning (TL) based method to leverage large-scale disease GWAS summary statistics and individual-level pharmacogenomics (PGx) data to predict drug response

## Tutorial
### To use PRS-PGx-TL-M1, M2, M3, or M4
#### Step 1: inner layer CV
```
Rscript s1.R [file for PRS weights from disease GWAS] [file for phenotype and covariates] [file for genotype] [file for SNP information] [initial values] [number of total snps with non-zero effects] [path for outputs in s1]
```
- **file for PRS weights from disease GWAS:** The following columns are required: `chr`, `SNP`, `BP`, `Eff`, `Ref`, `Beta`, which represent chromosome, SNP, base pair position, effect allele, reference allele, and beta coefficient, respectively. Column names are needed.
- **file for phenotype and covariates:** The following columns are required: `ID`, `Y`, covariates (including `Tr`), `prs_g`, `prs_gt`, which represent the ID for each individual, the drug response phenotype to be predicted, other covariates (must have the treatment variable `Tr`, the PRS calculated from the weights from disease GWAS, the product of PRS and treatment `prs_g*Tr`. Column names are needed.
- **file for genotype:** The genotype matrix of individual x SNP. Row names are ID and column names are SNP.
- **file for SNP information:** Allele info for the SNPs in genotype file. The following columns are required: `SNP`, `Ref`. Column names are needed.
- **initial values:** `PRS` or `zero`, indicating the starting values of the predictive effects.
- **number of total snps with non-zero effects:** The total number of SNPs in PRS weights file that have non-zero effects.
- **path for outputs:** For example, `/Mypath/result`. If step 1 is performed on each chromosome separately, please save the output as `/Mypath/result_1`,`/Mypath/result_2`...`/Mypath/result_22`.


#### Step 2: parameter tuning
```
Rscript s2.R [file for phenotype and covariates] [initial values] [path for outputs in s1] [path for outputs in s2] [indicator of whether files for all 22 chromosomes are separated]
```
#### Step 3: rerun the algorithm and get the output with the best parameter

#### Step 4: sum the PRS over all chromosomes for the testing samples (optional)


### To use PRS-PGx-TL-M5 or M6
