# Microarray Differential Expression Analysis 

An R-based bioinformatics pipeline utilizing `limma` to perform differential gene expression analysis on the NCBI GEO dataset **[GSE70970](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE70970)**. 

## 🧬 Biological Context
This pipeline analyzes **GSE70970**, a dataset containing comprehensive microRNA/transcriptomic profiling of **Nasopharyngeal Carcinoma (NPC)** specimens. The primary biological objective of this script is to identify genomic signatures that differentiate patient samples based on clinical outcomes—specifically comparing patients with **Metastasis** versus those with **No_Metastasis**.

## ⚙️ Prerequisites
To run this pipeline, you will need **R (>= 4.0.0)** and the following Bioconductor/CRAN packages installed:
*   `limma` (Linear Models for Microarray Data)
*   `GEOquery` (For fetching the dataset directly from NCBI GEO)
*   `dplyr` / `tidyverse` (For data wrangling)
*   `ggplot2` (For generating Volcano plots)
*   `pheatmap` (For hierarchical clustering heatmaps)

*Note: You can install the Bioconductor packages using `BiocManager::install(c("limma", "GEOquery", "pheatmap"))`.*

## 🛠️ Pipeline Workflow
The analysis is automated through a 5-step workflow:

1. **Data Acquisition & Extraction:** Automatically downloads and formats the raw series matrix file for GSE70970 using `GEOquery`.
2. **Clinical Metadata Parsing:** Extracts phenotype data from the GEO object and parses the clinical traits to classify patient samples into distinct biological groups (`Metastasis` vs. `No_Metastasis`).
3. **Normalization & Linear Modeling:** Applies array normalization (if not pre-normalized) and fits a linear model using the `lmFit` and `eBayes` functions from the `limma` package to assess differential expression.
4. **Data Tabulation:** Filters the results based on False Discovery Rate (FDR) and Log2 Fold Change (Log2FC) thresholds to generate comprehensive data tables for all genes, as well as isolated tables for significantly upregulated and downregulated genes.
5. **Data Visualization:** Generates publication-ready, high-resolution visualizations for the top 50 differentially expressed genes.

## 📊 Expected Outputs
Upon successful execution, the script will generate a local `/results` directory containing:

### Data Tables (.csv)
*   `all_differential_genes.csv`: The complete `topTable` output with unadjusted p-values, adjusted p-values (FDR), and Log2FC.
*   `upregulated_genes.csv`: Filtered list of significantly overexpressed genes in the Metastasis group.
*   `downregulated_genes.csv`: Filtered list of significantly underexpressed genes in the Metastasis group.

### Visualizations (.png / .pdf)
*   `volcano_plot.png`: A scatter plot highlighting genes with significant fold changes and high statistical significance.
*   `top50_heatmap.png`: A hierarchical clustering heatmap showing the expression profile of the top 50 most significant genes across all patient samples.

## 🚀 Usage
Clone this repository, set your working directory to the project folder in RStudio, and source the main analysis script:

```R
source("analysis_script.R")
```
*The script will automatically download the required GEO data into a temporary directory, so no manual dataset downloading is required.*