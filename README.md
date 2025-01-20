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
- **path for outputs in s1:** For example, `/Mypath/s1_result`. If step 1 is performed on each chromosome separately, please save the outputs as `/Mypath/s1_result_1`,`/Mypath/s1_result_2`...`/Mypath/s1_result_22`.


#### Step 2: parameter tuning
```
Rscript s2.R [file for phenotype and covariates] [initial values] [path for outputs in s1] [path for outputs in s2] [indicator of whether files for all 22 chromosomes are separated]
```
- **file for phenotype and covariates:** The following columns are required: `ID`, `Y`, covariates (including `Tr`), which represent the ID for each individual, the drug response phenotype to be predicted, other covariates (must have the treatment variable `Tr`. Column names are needed.
- **initial values:** `PRS` or `zero`, indicating the starting values of the predictive effects.
- **path for outputs in s1:** The output from step 1. For example, `/Mypath/s1_result`. If step 1 is performed on each chromosome separately and the outputs are saved as `/Mypath/s1_result_1`,`/Mypath/s1_result_2`...`/Mypath/s1_result_22`, just need to input `/Mypath/s1_result` here and the algorithm will add `_chr` automatically.
- **path for outputs in s2:** The output from step 2. For example, `/Mypath/s2_result`.
- **indicator of whether files for all 22 chromosomes are separated:** `yes` or `no`, indicating whether step 1 is performed on all chromosomes or on each chromosome separately.

#### Step 3: rerun the algorithm and get the output with the best parameter
```
Rscript s3.R [file for PRS weights from disease GWAS] [file for phenotype and covariates] [file for genotype] [file for SNP information] [initial values] [number of total snps with non-zero effects] [criterion] [path for outputs in s2] [path for outputs in s3]
```
- The inputs `file for PRS weights from disease GWAS`, `file for phenotype and covariates`, `file for genotype`, `file for SNP information`, `initial values`, `number of total snps with non-zero effects` are the same as those in `s1.R`.

#### Step 4: sum the PRS over all chromosomes for the testing samples (optional)


### To use PRS-PGx-TL-M5 or M6
