----

## Human Mortality Curve <sup>[2]</sup>

![bg left 90%](../../img/module_2/image1.jpg)

- Monogenic diseases are most commonly expressed in early childhood and later in life due to strong selection against disease expression during peak reproductivity age.
- After puberty, most genetic diseases are polygenic and only lead to disease expression when combined with other "nongenetic" triggers—like lifestyle or environmental factors.
<!--
- Monogenic diseases are most common in early childhood and then again later in life, with fewer cases during the reproductive years (young adulthood) due to strong selection against these diseases when they appear at an age that could affect an individual’s ability to reproduce.
- After puberty, most genetic diseases that show up are not due to monogenic (single-gene) causes alone. Instead, they’re often due to more complex genetic factors that only lead to disease when combined with other "nongenetic" triggers—like lifestyle or environmental factors.
-->
[2]:(https://doi.org/10.1016/B978-0-12-812537-3.00001-9) "Pyeritz, R. E. Medicine in a genetic and genomic context. In Emery and Rimoin's Principles and Practice of Medical Genetics and Genomics (7th edn) (eds. Pyeritz, R. E., Korf, B. R. & Grody, W. W.) 1–20 (Academic Press, 2019)."

----

Below is an **integrated set of tables** that combines the **three main normalization strategies** (by library size, by distribution, and by controls) and includes details on commonly used **metrics** (RPKM, FPKM, TPM, CPM) under the library-size category.

---

## **1. Normalization by Library Size**

| **Metric/Method** | **Name/Description**                               | **Calculation**                                                         | **Purpose**                                                                                      |
|-------------------|---------------------------------------------------|------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Total Count**   | Basic library-size scaling                         | (Gene read count) / (Total reads in sample)                           | Adjusts each gene’s read count by the total number of reads in the sample.                        |
| **CPM**           | Counts Per Million                                 | (Gene read count × 10^6) / (Total mapped reads)                       | Normalizes only for sequencing depth (not gene length).                                           |
| **RPKM**          | Reads Per Kilobase (kb) per Million (single-end)  | (Read count × 10^6) / (Total reads × Gene length in kb)               | Normalizes for both library size and gene length; often used for single-end RNA-seq.             |
| **FPKM**          | Fragments Per kb per Million (paired-end)         | Same as RPKM but accounts for paired-end reads                        | Normalizes for library size and gene length in paired-end RNA-seq.                                |
| **TPM**           | Transcripts Per Million                            | (Read count / Gene length) ÷ (Sum of all (Read count / Gene length)) × 10^6 | Normalizes within a sample to allow better comparison of relative expression levels across genes. |

**When to Choose:**  
- When the total mRNA/cell remains equal or within the same range across different treatments/conditions (i.e., no large global shift in total expression).  
- Especially suitable when asymmetry is small and the primary difference across samples is in sequencing depth.

**Key Assumptions:**  
- The total expression (mRNA/cell) does not vary substantially across samples.  
- Scaling by total reads or library metrics is sufficient to correct for technical variation.

**Limitations:**  
- Cannot handle **large asymmetries** or **global shifts** in expression where the total mRNA/cell is truly different across conditions.

---

## **2. Normalization by Distribution**

| **Method**                     | **Key Idea**                                                                                                              |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **Quantile Normalization**     | Forces the distribution of gene expression values (e.g., read counts or log-transformed counts) to match across samples.  |
| **Median/Upper Quartile**      | Normalizes counts based on a specified quantile (e.g., 50th or 75th percentile) rather than the total number of reads.    |
| **TMM (Trimmed Mean of M-values)** | Trims extreme values (highly expressed genes) and calculates scale factors using average log-fold changes (M-values).   |
| **PoissonSeq / DEGES**         | Iteratively identifies non-differentially expressed (non-DE) genes and estimates scaling factors using those genes only.   |

**When to Choose:**  
- When there is **symmetry in sample sizes**, even if total mRNA differs across samples.  
- Appropriate if you expect a **balanced** number of up- and down-regulated genes.

**Key Assumptions:**  
- DE and non-DE genes behave similarly from a technical standpoint.  
- **Small asymmetry** (e.g., a few highly expressed genes) can be handled; but not a **global shift** (large asymmetry).

**Limitations:**  
- **Cannot correct large asymmetries** in expression where the entire distribution shifts significantly.  
- Relies on the assumption of a roughly equal number of up- and down-regulated genes.

---

## **3. Normalization by Controls**

| **Method**             | **Key Idea**                                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Using Control Genes** | Normalizes data based on a set of genes known (or assumed) to have **constant** expression across samples (non-DE).  |
| **Spike-in Controls**   | Employs external RNA molecules (spikes) added at a known concentration to each sample to adjust for technical biases.|

**When to Choose:**  
- When you have reliable **control genes** or spike-ins that are **unaffected** by the biological condition of interest.  

**Key Assumptions:**  
- Controls remain constant across treatments.  
- Controls **reflect technical factors** (e.g., batch effects, library prep variability) for the entire sample.

**Limitations:**  
- **Relies on the availability** and accurate behavior of appropriate controls.  
- Cannot handle **global shifts** in expression if controls do not represent the full gene expression distribution.

---

### Summary of Use-Cases

- **Library Size Normalization**  
  - Best if total mRNA/cell is comparable across samples.  
  - Commonly used metrics include **CPM, RPKM, FPKM, TPM**.

- **Distribution-Based Normalization**  
  - Ideal if sample sizes are symmetric (balanced) but total mRNA may differ.  
  - Methods like **Quantile Normalization, Median/Upper Quartile, TMM** help align distributions.

- **Control-Based Normalization**  
  - Chosen when **consistent controls** (genes or spike-ins) exist and behave reliably.  
  - Effective if those controls truly represent general technical variation.

Use these tables to pinpoint which approach and specific metric or algorithm suits your data scenario.

Here's the **final version**, ensuring **accuracy** and **precision** based only on the information you provided. The **Normalization by Distribution** table remains unchanged since you liked that version.

---

## **1. Normalization by Library Size**

> **“Normalization by library size should be chosen when the total mRNA remains equal or in the same range across different treatments/conditions despite any asymmetry.”**

| **Metric** | **Name**                                   | **Calculation**                                                     | **Purpose**                                                                                                    |
|------------|---------------------------------------------|---------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **RPKM**   | Reads Per Kilobase (kb) per Million         | (Read count × 10⁶) / (Total reads × Gene length in kb)            | Normalizes for sequencing depth and gene length (often for single-end data). |
| **FPKM**   | Fragments Per Kilobase per Million          | Same as RPKM but for paired-end reads                              | Accounts for paired-end sequencing data.                                     |
| **TPM**    | Transcripts Per Million                     | (Read count / Gene length) ÷ (Sum of all RPK values) × 10⁶         | Normalizes within a sample to allow better comparability of expression levels across genes.                     |
| **CPM**    | Counts Per Million                          | (Read count × 10⁶) / (Total mapped reads)                          | Normalizes only for sequencing depth (not gene length).                                                        |

---

## **2. Normalization by Distribution**

> **“Normalization by distribution is mostly useful if there is symmetry in sample sizes even if there are differences in total mRNA across samples. Normalization by distribution (and by testing) can handle differences in mRNA/cell in the case of a few highly expressed genes (small asymmetry), but not a global shift in expression (large asymmetry).”**

| **Method**                     | **Key Idea**                                                                                                              |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **Quantile Normalization**     | Forces the distribution of gene expression values (e.g., read counts or log-transformed counts) to match across samples.  |
| **Median/Upper Quartile**      | Normalizes counts based on a specified quantile (e.g., 50th or 75th percentile) rather than the total number of reads.    |
| **TMM (Trimmed Mean of M-values)** | Trims extreme values (highly expressed genes) and calculates scale factors using average log-fold changes (M-values).   |
| **PoissonSeq / DEGES**         | Iteratively identifies non-differentially expressed (non-DE) genes and estimates scaling factors using those genes only.   |

---

## **3. Normalization by Controls**

> **“When controls exist that behave consistently across different treatments/conditions, use normalization by controls.”**

| **Method**             | **Key Idea**                                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Using Control Genes** | Normalizes data based on a set of genes known (or assumed) to have **constant** expression across samples (non-DE).  |
| **Spike-in Controls**   | Uses known amounts of external RNA spikes (added to each sample) to determine and correct for technical biases. |

---

### **Key Takeaways**

1. **Library Size**  
   - Best when total mRNA/cell remains comparable across samples.  
   - Common metrics: **RPKM, FPKM, TPM, CPM**.

2. **Distribution**  
   - Useful if **sample sizes are symmetrical**, even if total mRNA differs.  
   - Handles **small asymmetry** but **not** a large, global shift.  
   - Methods: **Quantile Normalization, Median/Upper Quartile, TMM, PoissonSeq/DEGES**.

3. **Controls**  
   - Appropriate when **reliable controls** exist and do **not** change with conditions.  
   - Assumes controls accurately capture **technical variation**.  
   - Methods: **Control Genes, Spike-in Controls**.

---

This version **strictly adheres to the information you provided** while improving clarity and structure. Let me know if you need any final refinements! 🚀