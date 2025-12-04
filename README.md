# 📊 Time-Series Proteomics Analysis Pipeline

**Dataset:** *Selevsek et al., 2015* — DIA/SWATH-MS time-course protein abundance under osmotic stress

**Methods:** ANOVA · Repeated Measures ANOVA · LMM · LM · EMMeans · Pairwise Comparisons 

---

## 📁 Project Overview

This repository contains a fully reproducible **time-series proteomics analysis pipeline** implemented in R. The workflow analyzes protein abundance changes in *Saccharomyces cerevisiae* exposed to osmotic stress over six time points, using univariate statistical models and model-based pairwise comparisons.

The analysis follows the structure of a statistical proteomics report and includes:

* Data preprocessing & transformation
* Filtering and random protein selection
* One-way ANOVA
* Repeated Measures ANOVA
* Linear Mixed-Effects Models (LMM)
* Fallback Linear Models (LM)
* Model selection using ICC
* Nested LM comparison
* Pairwise comparisons (Tukey & EMMeans)
* Volcano plot for significant contrasts
* Extraction of significant proteins

All intermediate files (summary tables, model results, p-value tables, EMMeans outputs, etc.) are automatically saved as CSV outputs.

---
## Installation & Requirements

### ** Install Required R Packages**

```r
install.packages(c(
  "tidyverse", "lme4", "lmerTest", "ez", "performance", "cluster",
  "ggplot2", "ggVennDiagram", "emmeans"
))
```

### ** Ensure Files Are in the Working Directory**

* `Selevsek2015_DIA_Spectronaut_annotation.csv`
* `Selevsek2015.csv`
* `TIME_SERIES_DATA_ANALYSIS.Rmd`

---


## 📈 Analysis Steps

### **1️⃣ Data Preparation**

* Read metadata & protein abundance matrix
* Pivot to long format
* Merge annotation info
* Remove missing values and low-variance proteins

### **2️⃣ Protein Subsampling**

Random selection of 150 proteins for efficient modeling.

### **3️⃣ One-Way ANOVA**

* Per-protein ANOVA
* P-value distribution summary
* Full ANOVA table exported

### **4️⃣ Repeated Measures ANOVA**

* Biological replicate treated as within-subject factor
* Extraction of p-values, F-values, and model tables

### **5️⃣ Linear Mixed-Effects Modeling**

* LMM with random intercepts
* Check for singular fits
* Fallback to LM when appropriate
* Calculate ICC and determine best-fitting model

### **6️⃣ Final Model Selection**

* Select LMM or LM based on ICC ≥ 0.01
* Save p-values, AIC, ICC, and chosen model

### **7️⃣ Pairwise Comparisons**

* Tukey HSD for ANOVA
* EMMeans for LMM/LM with FDR correction
* Top proteins with the most significant contrasts

### **8️⃣ Volcano Plot**

Contrast: **T030 vs T000**

* log2FC calculated
* FDR-adjusted p-values
* Red = significant proteins

---

## Output Summary

The pipeline generates:

### Statistical Outputs

* ANOVA p-values and full tables
* RM ANOVA p-values and F-values
* LMM vs LM model selection
* ICC values for repeated measures
* Nested LM comparison results

### Pairwise Results

* Tukey pairwise tables
* EMMeans contrast tables
* Top proteins by significant timepoint changes

### Visualizations

* Venn diagram of significant proteins
* Model usage heatmap
* Volcano plot (T030 vs T000)
