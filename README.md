# Differential Expression and Co-expression Analysis of Tumor Tissue
## Statistical Analysis of RNA-seq Data in R

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![R 4.0+](https://img.shields.io/badge/R-4.0+-blue.svg)](https://www.r-project.org/)

---

## Project Overview

This project demonstrates rigorous statistical analysis of RNA-sequencing data to identify genes differentially expressed between tumor and normal tissue samples. Using negative binomial regression and principal component analysis, the work showcases proficiency in bioinformatics workflows, statistical modeling, and R programming for genomic data analysis.

**Key Methods:** Data normalization (CPM), quality control via PCA, differential expression testing with negative binomial models, multiple testing correction, co-expression network analysis

**Data:** Paired tumor-normal tissue samples (n=30 samples, 4,568 genes)

**Outcome:** Identified significantly differentially expressed genes between tumor and normal tissue, with rigorous statistical validation and biological interpretation

---

## Research Context

RNA-sequencing (RNA-seq) has become the gold standard for measuring gene expression across the entire transcriptome. Differential expression analysis identifies genes whose expression levels change systematically between experimental conditions - in this case, tumor versus normal tissue. Such analyses form the foundation of molecular biology research, informing our understanding of disease mechanisms and potential therapeutic targets.

**Statistical Challenge:** RNA-seq data presents unique analytical challenges:
- **Count data:** Discrete read counts rather than continuous measurements
- **Overdispersion:** Variance exceeds mean, violating Poisson assumptions
- **Technical variation:** Library size differences across samples require normalization
- **Multiple testing:** Thousands of genes tested simultaneously inflates false discovery rates

This analysis demonstrates appropriate statistical methods to address each challenge.

---

## Methods

### Data Preprocessing and Quality Control

**Library size normalization:** Raw read counts were normalized to Counts Per Million (CPM) to account for varying sequencing depth across samples:

```
CPM = (raw count / library size) × 1,000,000
```

**Variance-stabilizing transformation:** Log2 transformation applied after adding pseudocount to handle zero values and stabilize variance across expression range.

**Quality control procedures:**
- Outlier sample detection via boxplot examination and PCA
- Paired sample integrity verification  
- Low-expression gene filtering to reduce noise

**Principal Component Analysis:** Used to identify major sources of variation in the data:
- PC1 captured 30.8% of variance, clearly separating tumor from normal samples
- Correlation analysis with technical variables (library size) to detect batch effects
- Elbow plot examination to determine effective dimensionality

### Differential Expression Analysis

**Statistical model:** Negative binomial regression selected over Poisson due to observed overdispersion in count data. The model accounts for:
- Tissue type (tumor vs. normal) as primary predictor
- Patient ID as blocking factor (paired design)
- Gene-specific dispersion parameters

**Model specification:**
```
log(μ) = β₀ + β₁(tissue) + β₂(patient)
```

where μ is the expected count for a given gene.

**Multiple testing correction:** Benjamini-Hochberg procedure applied to control false discovery rate at 5% threshold.

### Co-expression Analysis

Beyond individual gene significance, correlation structure examined to identify:
- Gene modules with coordinated expression patterns
- Potential functional relationships between genes
- Network architecture differences between tissue types

---

## Key Findings

**Tissue separation:** Principal Component Analysis revealed strong systematic differences between tumor and normal samples, with PC1 serving as the primary discriminant axis. This biological signal dominated technical variation, confirming data quality.

**Differential expression:** Multiple genes showed statistically significant expression changes between tumor and normal tissue after multiple testing correction. Effect sizes (log fold-changes) ranged from subtle to dramatic, reflecting diverse biological roles.

**Methodological validation:** Comparison of mean-variance relationships confirmed appropriateness of negative binomial over Poisson model. Model diagnostics revealed no substantial overfitting or collinearity issues.

---

## Technical Implementation

### Analysis Workflow

1. Data loading and structure examination
2. Library size calculation and CPM normalization  
3. Log transformation for variance stabilization
4. Quality control and outlier detection
5. Principal component analysis and visualization
6. Negative binomial model fitting for each gene
7. Statistical significance testing with FDR correction
8. Results visualization (heatmaps, volcano plots)

### R Packages Used

- **tidyverse:** Data manipulation and visualization
- **MASS:** Negative binomial regression (`glm.nb`)
- **pheatmap:** Heatmap generation
- **knitr/rmarkdown:** Reproducible reporting

### Reproducibility

Complete analysis code provided in R Markdown format with:
- Inline explanatory comments
- Narrative text explaining statistical choices
- Embedded visualizations with figure captions
- Computational environment documentation

---

## Files in This Repository

```
├── README.md                                    # This file
├── LICENSE                                      # MIT License
├── expression_analysis_rmd_final.Rmd           # Complete R Markdown analysis
├── expression_analysis_report_final.pdf        # Compiled analysis report
├── data/
│   └── Coursework_Data.Rdata                   # RNA-seq count matrix and metadata
└── outputs/
    ├── figures/                                 # All generated visualizations
    └── results/                                 # Statistical results tables
```

---

## Running the Analysis

### Prerequisites

- R version 4.0 or higher
- RStudio (recommended for R Markdown)
- Required R packages (install with commands below)

### Installation

```r
# Install required packages
install.packages(c("tidyverse", "MASS", "pheatmap", "knitr", "rmarkdown"))
```

### Execution

```r
# Open R Markdown file in RStudio
# Click "Knit" button to generate HTML/PDF report
# Or run from command line:
rmarkdown::render("expression_analysis_rmd_final.Rmd")
```

Analysis completes in approximately 5-10 minutes on a standard laptop.

---

## Statistical Rigor Demonstrated

This project showcases several key statistical competencies:

✅ **Appropriate model selection:** Negative binomial chosen over Poisson based on data properties  
✅ **Multiple testing correction:** FDR control via Benjamini-Hochberg procedure  
✅ **Paired design handling:** Patient-level blocking to account for within-subject correlation  
✅ **Quality control:** PCA-based outlier detection and technical variable assessment  
✅ **Diagnostic checking:** Model fit evaluation and assumption verification  
✅ **Reproducible workflow:** Complete code with documentation and narrative

---

## Connections to Broader Research

While this analysis focused on a specific tumor-normal comparison, the statistical framework generalizes to:

- **Drug response studies:** Identifying genes modulated by therapeutic interventions
- **Disease progression:** Characterizing molecular changes across disease stages  
- **Biomarker discovery:** Finding genes predictive of clinical outcomes
- **Precision medicine:** Stratifying patients based on molecular profiles

The methodological rigor demonstrated here translates directly to other high-dimensional biological data contexts including proteomics, metabolomics, and epigenomics.

---

## Limitations

**Data scale:** Analysis based on 30 samples provides limited statistical power for detecting small effect sizes. Larger cohorts would enable more robust inference.

**Single tissue type:** Findings specific to the analyzed tumor type; generalization to other cancers requires additional validation.

**Exploratory nature:** Analysis identifies associations but does not establish causal mechanisms. Functional validation would require experimental follow-up.

**Computational scope:** Focused on standard differential expression; more advanced methods (e.g., trajectory analysis, spatial transcriptomics) could provide additional biological insight.

---

## Project Provenance

**Author:** Riya Shet  
**Affiliation:** MSc Health Data Science, University of Birmingham  
**Course:** Statistical Methods for Health Data Science  
**Date:** January 2026  
**Status:** Completed coursework project

**Research Interests:** Statistical methods for genomic data, machine learning for healthcare applications, precision medicine

---

## License

**Code and documentation:** MIT License  
**Data:** Provided for educational purposes only

If you use or adapt this analysis methodology, please cite this repository.

---

## Contact

**Riya Shet**  
MSc Health Data Science Student  
University of Birmingham

GitHub: [@riyashet-hds](https://github.com/riyashet-hds)

---

**Repository Status:** Complete | Educational demonstration of bioinformatics workflow
