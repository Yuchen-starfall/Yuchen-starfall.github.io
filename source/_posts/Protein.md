---
title: Methods in Protein Chemistry
date: 2024-12-10 15:00
categories: BIO-2000-Molecular_biology
tags:
    - "Protein"
    - "course"
excerpt: false
---

## Foundation

### Protein purification

Isolating a specific protein from a cell for further study

Protein separation

* Different solubility -- 盐析（salting out）
* Different size 
  * Centrifugation（Density Gradient Centrifugation）
  * Dialysis（透析）
  * Size Exclusion (gel-filtration) chromatography（色谱）
  * Native PAGE
* Different charges
  * Ion-exchange chromatography
  * Two-dimensional electrophoresis
* Different ligandbinding
  * Affinity chromatography（Hi-His、Flag-MAb、GST-Glu、生物素-链霉）
* Difference surface features
  * Hydrophobic chromatography

**Goal: To set minimum objectives for purity and quantity, maintenance of** biological activity and economy in terms of money and time. **KEEP IT SIMPLE！**

**Develop analytical assays** for fast detection of protein activity/recovery and critical contaminants.

### Protein-mediated interactions

* Yeast two hybrid
  * DNA-binding domain + transcriptional activation domain (BAIT, captured prey)
  * Transcription of reporter gene
* Bimolecular fluorescence complementation (BiFC)
  * Two non-fluorescent fragments (YN and YC) of the yellow fluorescent protein (YFP) are fused to putative interaction partners (A and B)
* APEX
  * 生物素标记互做蛋白
  * POL-Peroxidase（过氧化物酶） + Biotin-phenol（生物素偶联苯酚）+ 过氧化物酶 --> 离POL近的蛋白标记上生物素
* Fluorescence resonance energy transfer (FRET)
  * A荧光蛋白的激发光频率在B荧光蛋白入射光频率内
* Size-exclusion Chromatography(SEC)
  * 互做蛋白的大小改变。洗脱时间提前
* Light scattering（散射）
  * Multi-angle static light scattering(MALS)
  * Dynamic light scattering (DLS)
* Mass photometry
* Pull down and Co-IP
  * Pull-down通过将融合标签的蛋白固定在载体上以捕获其结合的相互作用蛋白；Co-IP则利用特异性抗体从细胞裂解液中富集目标蛋白及其复合物中的结合蛋白
* Far-western blot
  * 一抗二抗
* Electrophoreticmobility shift assay(EMSA)、
* Isothermal Titration Calorimetry (ITC)
* Surface Plasmon Resonance (SPR)

### Protein engineering

1. Directed evolution -- 多色荧光蛋白
   * **Mimic natural evolution.** No structural or mechanistic information required. Large library size and high throughput selection /screening techniques needed
   * Random mutation（error prone PCR、nucleoside analogs）
   * Recomination（DNA shuffling）
   * Phage display（噬菌体展示）
     * Make a combinatorial library of genes of interest
     * Put genes into a vector so that each gene product is expressed on the surface of a bacteriophage
     * Take collection of phage and select those with desired properties (e.g., binding to something)

2. Rational design
   * Require structural and mechanistic information
   * Computer design --> Site–directed mutagenesis --> Biochemical assays to check the stability and activity

3. De novo design
   * Computational design from scratch
   * The design of a functional binder (magenta) to a target protein (grey)

从有到优：Directed evolution、Rational design

从无到有：De novo design

### Structural biology

* X-ray based structural methods (crystallography（晶体学）, coherent imaging（相干衍射）, scattering（小角衍射）)

* CryoElectron Microscopy (Cryo-EM)
  * Single particle analysis

* Nuclear magnetic resonance (NMR)
  * 核磁共振，是指核**磁矩不为零的原子核**，在外磁场的作用下，核自旋能级发生塞曼分裂（Zeeman Splitting），共振吸收某一特定频率的射频辐射的物理过程。

* Structural prediction