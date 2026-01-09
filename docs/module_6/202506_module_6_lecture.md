---
marp: true
-style: @import url('https://unpkg.com/tailwindcss@^2/dist/utilities.min.css');
theme: base-theme
style: |
img {
  display: block;
  height: auto;
  margin: auto};
markdown: 
  - html: true

---
<style scoped>
h1 {
  font-weight: bold;
  font-size: 48;
}
</style>

# Module 6: Differential Gene Analysis (Part 1)

---

## Key Concepts

- Differential gene analysis
- Read count normalization
- Read count transformation
- Gene filtering strategies

---

## Differential gene analysis

- The aim of a differential gene analysis is to identify genes with difference in expression patterns under different experimental conditions (gene(s) versus condition(s) and vice versa) for a set of samples.  
- By asking “which genes change and by how much?” and then mapping those changes to **pathways, processes, and regulatory mechanisms**, we can generate hypotheses about the underlying biological mechanisms.
  - **Disease mechanisms** (e.g., identifying driver genes in cancer)  
  - **Therapeutic targets** or potential drug mechanisms  
  - **Biomarker discovery** for diagnosis and prognosis  
  - **Fundamental biology** of development, stress responses, or adaptation.

---

<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 0.3; padding-right: 10px;background-color:rgb(255, 255, 255);" markdown="span">

<p style="text-align:center"><img src="image-2.png" alt="img" width = "300px"></p>
<p style="text-align:center"><img src="image-3.png" alt="img" width = "300px"></p>

[Zeng *et al.* 2022](https://doi.org/10.1080/21655979.2022.2073943)

</left>
<right id="col_right" style="flex: 0.7; padding-left: 10px;background-color:rgb(255, 255, 255);" markdown="span">

### Which genes are up- or down-regulated in a given condition?

**Question**: Under condition A vs. condition B (e.g., treated vs. untreated), which genes show significant changes in expression levels?  

- The treatment can be drug exposure, knock-out mutation, or any external stimulus
- Identifying up-regulated genes can point toward processes or pathways that are activated under specific conditions, while down-regulated genes might indicate suppression or reduced activity of certain pathways.

</right>
</main>

---

### What pathways or biological processes are affected?

**Question**: Are the significantly differentially expressed genes enriched in specific functional categories, pathways, or Gene Ontology terms?  

- DGE results often feed into **gene set enrichment analysis (GSEA)** or pathway analysis (gProfiler) to reveal broader biological programs at play—like inflammation, cell cycle regulation, or metabolic shifts.

<p style="text-align:center"><img src="image-1.png" alt="img" width = "600px"></p>

[Zeng *et al.* 2022](https://doi.org/10.1080/21655979.2022.2073943)

---
<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 0.35; padding-right: 10px;background-color:rgb(255, 255, 255);" markdown="span">

![alt text](image-4.png)
[Zhang *et al.* 2019](https://doi.org/10.1371/journal.pcbi.1007435)

</left>
<right id="col_right" style="flex: 0.55; padding-left: 10px;background-color:rgb(255, 255, 255);" markdown="span">

### How does gene expression change over time (time-course experiments)?

- **Question**: What genes are differentially expressed at early vs. late stages of a response, disease progression, or development?  
  - Time-course DGE studies can reveal **dynamic gene expression trends** that can help identify early-response genes, late-stage markers, or transitions in biological processes.

</right>
</main>

---

### Are there biomarker candidates for disease or treatment response?

- **Question**: Which genes consistently show differential expression in a disease state (e.g., tumor vs. normal tissue) or in response to a therapy?  
  - Such genes may serve as **potential biomarkers** for diagnostic, prognostic, or therapeutic monitoring purposes (e.g., predicting drug resistance or disease recurrence).

<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 0.75; padding-right: 10px;background-color:rgb(255, 255, 255);" markdown="span">

<p style="text-align:center"><img src="image-5.png" alt="img" width = "600px"></p>

</left>

<right id="col_right" style="flex: 0.5; padding-left: 10px;background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

LINC00853 expression in the nontumor and the HCC cohorts in three HCC RNA-Seq datasets (TCGA_LIHC, GSE94660, and GSE124535).

</right>
</main>

---

<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 0.7; padding-right: 1px;background-color:rgb(255, 255, 255); font-size:20pt" markdown="span">

### Can we classify or subtype biological samples based on gene expression profiles?

- **Question**: In a cohort of samples (e.g., different cancer subtypes), which sets of genes distinguish one subtype from another?  
  - Identifying **signature genes** for subtypes can guide more personalized treatment strategies

- **Example**: Different subtypes of breast cancer have very different expression profiles. These expression profiles are associated with different patient outcomes and with different treatment protocols. Different subtypes of breast cancer can be distinguished by using differential transcript isoform expression ([Stricker *et al.* 2017](https://doi.org/10.1371/journal.pgen.1006589)).

</left>

<right id="col_right" style="flex: 0.3; padding-left: 1px;background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

<p style="text-align:center"><img src="image-7.png" alt="img" width = "300px"></p>

<p style="text-align:center"><img src="image-8.png" alt="img" width = "300px"></p>

</right>
</main>



----

## DGE Tools

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

| **Tool**   | **Statistical Model**                                                                            | **Key Strengths**                                                                                                                                                                                                                             | **When to Use**                                                                                                                                                                                                                                                               |
|------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DESeq2** | - Negative binomial with empirical Bayesian shrinkage of dispersion and fold changes <br> - Based on the hypothesis that most genes are not DE               | - Better handling of overdispersion  <br>- Good documentation and built-in plotting (MA plots, PCA)  <br>- Shrinkage of fold changes helps stabilize LFC for low-count genes                                                                                           | - Moderate sample sizes (≥3 replicates/condition) <br>- Typical RNA-seq designs (two-group or multi-factor) <br>- Ideal if you want an easy-to-follow pipeline with built-in diagnostics|

</tb>

----

## DGE Tools

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

| **Tool**   | **Statistical Model**                                                                            | **Key Strengths**                                                                                                                                                                                                                             | **When to Use**                                                                                                                                                                                                                                                               |
|------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **edgeR**  | - Negative binomial with empirical Bayes estimation of dispersion <br>- Based on the hypothesis that most genes are not DE                                  | - Highly flexible for complex or unbalanced designs  <br>- Known to perform robustly even with smaller sample sizes  <br>- Deep configurability for normalization, dispersion, and model setup                                                                                       | - Complex experimental designs (time series, multi-factor) <br>- Smaller datasets (though more replicates is still better) <br>- Prefer a “light-weight” approach with fine-grained control                                                                                     |

</tb>

----

## DGE Tools

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

| **Tool**   | **Statistical Model**                                                                            | **Key Strengths**                                                                                                                                                                                                                             | **When to Use**                                                                                                                                                                                                                                                               |
|------------|---------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **limma** (with **voom**) | Linear models with empirical Bayes shrinkage of variance estimates (after voom transformation)    | - Stable release (works with microarray data)  <br>- Good for large datasets and complex designs  <br>- Fast and memory-efficient; integrates well with other limma functions (e.g., contrasts, gene set testing)                                                        | - Already familiar with limma or microarray workflows <br>- Large sample sizes or multi-factor, repeated-measures designs <br>- Looking for flexible linear modeling framework and advanced downstream analyses (e.g., GSEA, contrasts)                                          |

</tb>

----

## Read Count Normalization: Why do we need to do this?<sup>[2]</sup>

<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 0.35; padding-right: 10px;background-color:rgb(255, 255, 255); font-size:20pt" markdown="span">

<p style="text-align:center"><img src="image-14.png" alt="img" width = "350px"></p>

</left>

<right id="col_right" style="flex: 0.65; padding-left: 10px;background-color:rgb(255, 255, 255);font-size:22pt" markdown="span">

- The correct normalization method to use depends on which assumptions are valid for the biological experiment.
- Incorrect normalization leads to problems in downstream analysis, such as inflated false positives, that mean results cannot be trusted.
- **Example**: A small number of highly expressed genes creates the appearance that non-DE are DE, but the false DE calls may be corrected by normalizing read counts so that the expression levels of non-DE genes are equivalent.

</right>
</main>

[2]:(https://doi.org/10.1093/bib/bbx008) "Ciaran Evans, Johanna Hardin, Daniel M Stoebel, Selecting between-sample RNA-Seq normalization methods from the perspective of their assumptions, Briefings in Bioinformatics, Volume 19, Issue 5, September 2018, Pages 776–792"

---

## Read Count Normalization: Why do we need to do this?<sup>[2]</sup>

<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 0.6; padding-right: 10px;background-color:rgb(255, 255, 255); font-size:20pt" markdown="span">

<p style="text-align:center"><img src="image-15.png" alt="img" width = "700px"></p>

</left>

<right id="col_right" style="flex: 0.4; padding-left: 10px;background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

- In the case of a global shift in expression, it may appear that DE genes are non-DE or that up-regulated genes are down-regulated.

- It is necessary to take into account the differences in overall expression between conditions.

</right>
</main>

----

### Read Count Normalization: Normalization by Library Size<sup>[2]</sup>

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

|    | **Details** |
|---------------|------------|
| **Use Case**  | When the total mRNA remains equal or within the same range across different treatments/conditions, even if there is some asymmetry. |
| **Assumptions** | - Total mRNA/cell is consistent across conditions. <br> - Differences in sequencing depth are the primary technical variability. |
| **Limitations** | - Cannot handle global shifts in expression (large asymmetry). <br> - Assumes minimal variability in the total mRNA/cell across samples. |

</tb>

<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 1; padding-right: 10px;background-color:rgb(255, 255, 255); font-size:20pt" markdown="span">

<p style="text-align:center;"><img src="image-17.png" alt="img1" width = "span"></p>

</left>

<mid style="flex: 1; padding-right: 10px;background-color:rgb(255, 255, 255); font-size:20pt" markdown="span">

<p style="text-align:center;"><img src="image-18.png" alt="img2" width = "300px"></p>

</mid>

<right id="col_right" style="flex: 1; padding-left: 10px;background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

<p style="text-align:center;"><img src="image-19.png" alt="img3" width = "300px"></p>

</right>
</main>

----

### Read Count Normalization: Normalization by Library Size

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:18pt" markdown="span">

| **Metric** | **Name**                                   | **Calculation**                                                     | **Purpose**                                                                                                    |
|------------|---------------------------------------------|---------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **RPKM**   | Reads Per Kilobase (kb) per Million         | (Read count × 10⁶) / (Total reads × Gene length in kb)            | Normalizes for sequencing depth and gene length (often for single-end data). |
| **FPKM**   | Fragments Per Kilobase per Million          | Same as RPKM but for paired-end reads                              | Accounts for paired-end sequencing data.                                     |
| **TPM**    | Transcripts Per Million                     | (Read count / Gene length) ÷ (Sum of all RPK values) × 10⁶         | Normalizes within a sample to allow better comparability of expression levels across genes.                     |
| **CPM**    | Counts Per Million                          | (Read count × 10⁶) / (Total mapped reads)                          | Normalizes only for sequencing depth (not gene length).                                                        |

</tb>

---

### Read Count Normalization: Normalization by Distribution<sup>[2]</sup>

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:16pt" markdown="span">

| | **Details** |
|---------------|------------|
| **Use Case**  | When there is symmetry in sample sizes, even if total mRNA levels differ across conditions. |
| **Assumptions** | - DE & non-DE genes behave similarly (technical effects are the same). <br> - Balanced expression: approximately equal numbers of up- and down-regulated genes across conditions. |
| **Advantages** | Can handle small asymmetry (e.g., a few highly expressed genes) or differences in total mRNA/cell. |
| **Limitations** | Fails to correct global shifts in expression (large asymmetry). |

</tb>
<main id="main" style="display: flex; border: 1px; padding: 1px;">

<left style="flex: 1; padding-right: 10px;background-color:rgb(255, 255, 255); font-size:20pt" markdown="span">

<p style="text-align:center;"><img src="image-17.png" alt="img1" width = "300px"></p>

</left>

<right id="col_right" style="flex: 2; padding-left: 10px;background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

<p style="text-align:center;"><img src="image-20.png" alt="img3" width = "800px"></p>

</right>

</main>

---

### Read Count Normalization: Normalization by Distribution<sup>[2]</sup>

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:20pt" markdown="span">

| **Method**                     | **Key Idea**                                                                                                              |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **Quantile Normalization**     | Forces the distribution of gene expression values (e.g., read counts or log-transformed counts) to match across samples.  |
| **Median/Upper Quartile**      | Normalizes counts based on a specified quantile (e.g., 50th or 75th percentile) rather than the total number of reads.    |
| **TMM (Trimmed Mean of M-values)** | Trims extreme values (highly expressed genes) and calculates scale factors using average log-fold changes (M-values).   |
| **PoissonSeq / DEGES**         | Iteratively identifies non-differentially expressed (non-DE) genes and estimates scaling factors using those genes only.   |

</tb>

---

### Read Count Normalization: Normalization by Controls<sup>[2]</sup>

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:16pt" markdown="span">

|    | **Details** |
|---------------|------------|
| **Use Case**  | When suitable controls exist that remain unaffected by biological conditions and behave consistently across samples. |
| **Assumptions** | - Controls exist and are non-DE in the context of the experiment. <br> - Controls reflect technical effects for all genes. |
| **Advantages** | Corrects for variations in sequencing depth and technical effects using robust controls. |
| **Limitations** | - Requires reliable and representative controls. <br> - Cannot correct global shifts in expression if controls do not reflect all genes. |

</tb>

<div class="row" style= "display: flex;">
  <div class="column">
  <p style="text-align:center;"><img src="image-22.png" alt="img3" width = "span"></p>
    </div>
  <div class="column">
  </div>
  <div class="column">
    <p style="text-align:center;"><img src="image-21.png" alt="img3" width = "span"></p>
  </div>
  <div class="column">
      <p style="text-align:center;"><img src="image-24.png" alt="img3" width = "span"></p>
  </div>
</div>

----

### Read Count Normalization: Normalization by Controls<sup>[2]</sup>

| **Method**             | **Key Idea**                                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Using Control Genes** | Normalizes data based on a set of genes known (or assumed) to have **constant** expression across samples (non-DE).  |
| **Spike-in Controls**   | Uses known amounts of external RNA spikes (added to each sample) to determine and correct for technical biases. |

----

## Read Count Transformation: Why do we need to do this?

- **RNA-seq count data is highly skewed** (due to differences in sequencing depth, expression levels, and variance).
- **Standard log transformation (log2(count + 1)) is not sufficient** due to heteroscedasticity (high variance for highly expressed genes), so we use **VST** and **rlog** to help stabilize variance

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:18pt" markdown="span">

| Feature                     | Variance Stabilizing Transformation (VST) | Regularized Log Transformation (rlog) |
|-----------------------------|-------------------------------------------|---------------------------------------|
| **Purpose**         | Stabilizes variance for high-count genes | Shrinks differences between low-count genes while preserving higher count relationships |
| **Assumes Variance-Mean Relationship?** | Yes, variance increases with mean expression | Yes, but applies stronger shrinkage for low counts |

</tb>

---

<tb id="tb" style="background-color:rgb(255, 255, 255);font-size:18pt" markdown="span">

| Feature                     | Variance Stabilizing Transformation (VST) | Regularized Log Transformation (rlog) |
|-----------------------------|-------------------------------------------|---------------------------------------|
| **Dataset size** | Optimized for large samples | Computationally expensive for large datasets |
| **Computational Speed** | Fast| Slower due to Bayesian shrinkage |
| **Handles Low-Count Genes Well?** | Partially, but less aggressive | Yes, applies stronger shrinkage |
| **Normalization** | Assumes normalized counts (DESeq2 size factors) | Assumes normalized counts (DESeq2 size factors) |
| **Use Case** | Large-scale RNA-seq datasets, differential expression analysis | Small RNA-seq datasets, noise reduction in low-count genes |

</tb>

----

## Gene Filtering Strategies

- Expression Threshold (Minimum Counts or CPM/TPM)
- Sample Proportion
- Variance or Coefficient of Variation (CV) Filtering
- Filtering by Group-Specific Expression

----

## Gene Filtering Strategies
### Expression Threshold (Minimum Counts or CPM/TPM)

- Remove genes that do not meet a minimum read count or transcripts per million (TPM) / counts per million (CPM) threshold in a certain fraction of samples.
- **Example**: Genes must have a CPM ≥ 1 or 2 in at least X samples, where X could be the size of the smallest experimental group
- Genes with extremely low expression are more prone to noise and can inflate multiple testing corrections.

----

## Gene Filtering Strategies
### Sample Proportion

- Retain only those genes that are “detected” (above a given expression threshold) in a specific percentage (e.g., 50%, 75%, etc.) of the samples, or in all samples of at least one condition.
- If a gene is detected in only one or two samples, it may not be informative across biological replicates or conditions.
- **Example**: A gene must have a minimum of 1 read per million in at least 50% of all samples

----

## Gene Filtering Strategies

### Variance or Coefficient of Variation (CV) Filtering

- Filter out genes whose expression values show very little variation across all samples (e.g., genes that are nearly constant).
- Genes that do not vary much are unlikely to be differentially expressed between conditions.
- Compute the standard deviation or CV of normalized expression across samples > remove genes below a certain variance threshold (e.g., “remove the bottom 20% of genes by variance”).

----

## Gene Filtering Strategies

### Filtering by Group-Specific Expression

- Ensure that a gene is expressed in at least one experimental group to a certain minimum level.
- Require that the gene has a minimum of X counts in at least Y replicates of at least one condition (e.g., “At least 5 counts in ≥2 samples in at least one group”).