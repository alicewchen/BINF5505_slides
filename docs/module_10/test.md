### **Slide: Understanding LOD Score in Linkage Analysis**

#### **Title: LOD Score – Measuring Genetic Linkage**

---

### **What is a LOD Score?**

- **LOD (Logarithm of the Odds) score** quantifies the likelihood of genetic linkage between a marker and a disease locus.
- It is the **logarithm of the likelihood ratio**, comparing:
  - The probability of **linkage** at a given recombination fraction (\(\theta\)).
  - The probability of **no linkage** (\(\theta = 0.5\)).

---

### **LOD Score Calculation**

\[
Z(x) = \log_{10} \left( \frac{L(x)}{L(\infty)} \right)
\]
Where:

- \( L(x) \) = Likelihood of the disease locus at position \( x \) on the marker map.
- \( L(\infty) \) = Likelihood of the disease locus being infinitely far from the marker.

---

### **Interpreting LOD Scores**

- **LOD ≥ 3.3** → Strong evidence for linkage (**genome-wide significance** at \( p = 0.05 \)).
- **LOD ≤ -2** → Evidence against linkage.
- **Multipoint LOD scores** generate a curve across a chromosome to identify the **likely position of a disease gene**.

---

### **Applications in Disease Gene Mapping**

- Historically used in **family-based studies** to identify **Mendelian disease genes**.
- Previously required **sequencing candidate regions**, but now **whole-genome sequencing (WGS)** allows rapid follow-up of suggestive linkage signals.
- Modern applications involve **combining linkage with GWAS and functional genomics**.

---

Would you like a **diagram** to visually explain LOD scores?
