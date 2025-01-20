# PRS-PGx-TL
A transfer learning (TL) based method to leverage large-scale disease GWAS summary statistics and individual-level pharmacogenomics (PGx) data to predict drug response

## Tutorial
### To use PRS-PGx-TL-M1, M2, M3, or M4
#### Step 1: inner layer CV
```
Rscript HBI.R [file for phenotype/DNA methylation] [Phenotype/CpG name] [file for genotype] [file for cell type proportions] [file for covariates] [path for outputs] \
distance=500000
```
- **Phenotype/CpG name:** The CpG to be tested should be specified, for example, `cg08730728`.
- **file for genotype:** Genotype file in VCF format. The individual IDs in the VCF file should match with other files.
- **file for cell type proportions:** The first column is `IID`, each of the remaining columns represents one cell type. Column names are needed.

#### Step 2: parameter tuning

#### Step 3: rerun the algorithm and get the output with the best parameter

#### Step 4: sum the PRS over all chromosomes for the testing samples (optional)


### To use PRS-PGx-TL-M5 or M6
