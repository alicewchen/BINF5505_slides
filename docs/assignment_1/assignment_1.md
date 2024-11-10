---
marp: true
-style: @import url('https://unpkg.com/tailwindcss@^2/dist/utilities.min.css');
theme: base-theme
style: |
img[alt$=">"] {
  float: right;}
img[alt$="<"] {
  float: left;};
img[alt$="><"] {
  display: block;
  height: auto;
  margin: auto;
  float: none!important;};
---
<style scoped>
h1 {
  font-weight: bold;
  font-size: 48;
}
</style>
# Module 2: Lab Assignment 1
---

## What is a genome browser? <sup>[1]</sup>

Genome browsers *integrate genomic sequence and annotation data* from different sources and provide a platform to search, browse, retrieve, and analyze genomic data.

They *differ from ordinary biological databases* in that they display data in a graphical format, with genome coordinates on one axis with annotations or space-filling graphics to show analyses of the genes, such as the frequency of the genes, their expression profiles, etc.


**What is meant by annotation of data?**

- Annotation means attaching biological information to sequences.


[1]:https://www.youtube.com/watch?v=s3JkAEAhkt8

---

## Importance of Genome Browser <sup>[1]</sup>

- *Supports text and sequence-based searches* that provide quick, precise access to any region of interest.
- *Visualize and browse entire genomes* with annotated data including gene prediction and structure, proteins, expression, regulation, variation, comparative analysis, etc. Annotated data is usually from multiple diverse sources.
- *View and interpret the many different types of data* that can be anchored to genomic positions. These include variation, transcription.
- Many large genomic projects also incorporate genome browsers into their web portals to enable users to easily search and view the data. These include:
    1. GTEx
    2. gnomAD

[1]:https://www.youtube.com/watch?v=s3JkAEAhkt8

---

## Direction of arrows: 5’ > 3’ of a gene <sup>[2]<\sup>
![image](../../img/assignment_1/image.png)
 
<br>
<br>

[2]: https://genome.ucsc.edu/training/education/fivePrime.html

---

## Find the UTRs <sup>[2]</sup>

![image](../../img/assignment_1/image%201.png)
 
<br>
<br>

[2]: https://genome.ucsc.edu/training/education/fivePrime.html

---

## Identify strand direction and exon <sup>[2]</sup>

![image](../../img/assignment_1/image%202.png)
 
<br>
<br>


[2]: https://genome.ucsc.edu/training/education/fivePrime.html

---

## Find disease variants using OMIM track

Different variants of PLP1 are associated with different disease states <sup>[3]</sup>
![image](../../img/assignment_1/image%203.png)
![image](../../img/assignment_1/image%204.png)

[3]: http://genome.ucsc.edu/s/education/hg19_PLP1

---

## Find tissue-specific gene expression using GTEx V8 track

![image](../../img/assignment_1/image%205.png)

> ### Tissue Specificity of Human Disease Module <sup>[4]</sup>
> - Disease-associated genes are more likely to exhibit tissue-specific expression than non-disease-associated genes 
> - The integration of gene expression, disease manifestation, molecular network connectivity, and tissue specificity data leads to better predictions of novel disease-gene candidates than any of these elements alone


[4]: https://doi.org/10.1038/srep35241 "Kitsak, M., Sharma, A., Menche, J. et al. Tissue Specificity of Human Disease Module. Sci Rep 6, 35241 (2016)."

---

## Find tissue-specific gene expression using GTEx V8 track

![image](../../img/assignment_1/image%206.png)


- How do gene expression at specific tissues relate to the clinically expressed symptoms of this disease?


---

## Locate regulatory elements using ENCODE Tracks<sup>[5]</sup>

![center](../../img/assignment_1/image%207.png)
![center](../../img/assignment_1/image%208.png) 
- Data is an overlay from **seven different cell lines**.

[5]: https://genome.ucsc.edu/s/alicewchen/hg38_KMT2A

---
## Locate regulatory elements using ENCODE Tracks<sup>[5]</sup>

![center](../../img/assignment_1/image%208.png)

- **H3K Tracks: Height represents intensity** of acetylation of lysine on the H3 histone.
    - Higher peaks = more acetylation
    - High histone acetylation often indicates regulatory elements.
- **DNase I Hypersensitivity Track:** peaks indicate potential regulatory or promoter regions

[5]: https://genome.ucsc.edu/s/alicewchen/hg38_KMT2A

---

## Find conserved regions using Conservation Tracks<sup>[5]</sup>

![center](../../img/assignment_1/image%209.png)
![center](../../img/assignment_1/image%2010.png)

- Highly conserved sequences often have important biological functions
    - Exons are highly conserved across species.
- Most pathogenic variants are located at conserved positions (high positive phyloP scores)<sup>[6]</sup>

[5]: https://genome.ucsc.edu/s/alicewchen/hg38_KMT2A
[6]: https://doi.org/10.1038/s41598-018-38189-9

---



## Lab Assignment 1 Instructions

- You are assigned to a group.  Each group is responsible for one genetic disease from Module 14.
- Use the gene of interest for your group's genetic disease to complete Lab Assignment 1.


---