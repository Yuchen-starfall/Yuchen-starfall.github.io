---
title: DNA metabolism
date: 2024-12-11 18:53
categories: BIO-2000-Molecular_biology
tags:
    - "DNA"
    - "course"
    - "Chromosome"
excerpt: false
---

## Foundation

### DNA multiple conformation

**A-DNA（高盐溶液或脱水的情况）, B-DNA（Waston和Crick）**, C-DNA, D-DNA, E-DNA, L-DNA, P-DNA,S-DNA, and **Z-DNA（CGCGCG寡聚体发现）**. triple-stranded DNA possibility（**Hoogsteen base pairing**）.

| Geometry attribute   | A-DNA        | B-DNA        | Z-DNA       |
| -------------------- | ------------ | ------------ | ----------- |
| Helix sense          | Right-handed | Right-handed | Left-handed |
| Rotation             | 32.7         | 34.3         | 60          |
| Bp/turn              | 11           | 10.5         | 12          |
| Rise/bp along axis   | 2.3          | 3.32         | 3.8         |
| mean propeller twist | +18          | +16          | 0           |

### Mechanical properties of DNA

* stretch
* bend（弯曲）
* twist（扭曲）
* writhe（扭动，区别twist例子是环）

### Chromatin and Chromosome

* Define

  * Chromatin（染色质）非分裂期

    染色质是染色体的松散状态，由DNA、组蛋白及其他蛋白质构成。它存在于细胞核内，看起来像一团纤维网络。在显微镜下，染色质可分为两种：

    * **Heterochromatin（异染色质）**：密集、转录活性低。
    * **Euchromatin（常染色质）**：松散、转录活性高。

  * Chromosome（染色体）

    染色体是染色质在细胞分裂期间高度凝缩的形式。染色体在分裂期中变得更紧凑，以便于细胞均匀分配遗传物质。染色体的必须元件：ARS（自主复制元件）、端粒、着丝粒序列

* Centromeric

  * 丝粒特异相关蛋白 （CENP）
  * 在多数真核生物中，着丝粒没有特异序列；典型的着丝粒由大片范围的重复 DNA 序列构成，这些重复序列相似却不完全相同
  * CENP-A（着丝粒特异相关蛋白A）是H3 的变体，是着丝粒染色质中组 蛋白的主要组成部分。也就是说，着丝粒染色质中核小体的组蛋白H3 大部分 被替换成了CENP-A，且排列在动粒附近（外周）的核小体都是CENP-A 组蛋 白，而排在里面的核小体是H3 组蛋白。

* Telomere

  * Distinguish intact telomeres from broken chromosomes
  * Facilitate the replication of the very end of the chromosom
  * Transcriptionally **repress** the genes near telomeres
  * Telomerase（端粒酶）反转录酶，能利用自身携带的RNA链作为模板，以反转录的方式催化合成模板后随链5’端DNA片段或外加重复单位，以维持端粒一定的长度，从而防止染色体缺失损伤

### DNA Polymerase

* Primer + Template + NTP + Mg2+

* Structure: 

  * Palm: catalytic site,(2 active sites)
  * Fingers: position the template,
  * Thumb: binds DNA,
  * processivity,
  * Exonuclease domain（外切酶）, 3’-5’(1 active site)
  * N-terminal domain: 5’-3’

* DNA replication--Bidirectional replication

  ![Test](img/img-DNA_metabolism/1.png)

* Topoisomerase&Helicase（拓扑异构、解旋）

* SSB

* DNA Clamp（DNA pol III必要组成）

* DNA Primase

* FEN1&ligase（切引物，补链）

  ![Test](/img/img-DNA_metabolism/2.png)

### DNA Damage

* 类型：
  * Damaged Base （Mis-Match）
  * Inter-strand Crosslink （最难处理）：双链断裂（DSBs）、单链断裂（SSBs）
* DNA Damage Response

  * RecA Filament (RecA蛋白丝状结构)

    * RecA是细菌中的一种关键蛋白，它在DNA损伤的修复中起重要作用。当DNA受到损伤，尤其是双链断裂时，RecA会与单链DNA结合，形成丝状结构。这种结构促进了同源重组修复，并启动SOS应激反应
  * LexA Autocleavage (LexA自裂解)
    * LexA是一种细菌中的转录抑制因子，通常抑制与DNA修复相关的基因。当RecA检测到DNA损伤后，它会激活LexA的自我裂解过程，使LexA失去活性，从而解锁SOS应激反应，启动DNA修复基因的表达。
    
  * Activating SOD Genes (激活SOD基因)
  
    *  SOD（超氧化物歧化酶）基因编码的酶负责清除超氧自由基（ROS，活性氧）。当DNA受损时，细胞通常会产生更多的ROS，进一步加剧损伤。激活SOD基因有助于减少ROS对DNA的破坏，保护细胞免受氧化应激。
*  DDR会通过抑制关键细胞周期检查点（如G1/S或G2/M）来给修复过程提供时间。例如：p53介导细胞周期停滞甚至诱导凋亡。

### DNA Repair

* Direct reversal
  * 植物中UV导致TT交联 -- 光裂合酶（Photolyase）吸收可见光（如蓝光）并将能量用于裂解UV引起的二聚体，恢复DNA正常结构
  * O-6-methylguanine-DNA methyltransferase -- m6G --> G
* Base excision repair
  * 识别：DNA糖基化酶（OGG1、UNG等）
  * 剪切：AP内切酶（APE1）
  * 合成酶：DNA聚合酶（Pol β）
  * 连接酶：DNA连接酶（Ligase III）
* Nucleotide excision repair
  * 全基因组修复（Global Genome Repair, GGR）-- XPC复合体
  * 转录偶联修复（Transcription-Coupled Repair, TCR）-- RNA聚合酶II暂停和 CSA/CSB蛋白辅助完成
* Translesion synthesis（跨损伤合成 -- 容错机制）
* Mismatch repair
* Double strand break repair
  * Recombination repair
  * Non-homologous end joining
* Inter strand cross-link repair
  * 主要：切开交联链引入单链断裂，通过核苷酸切除修复（NER）移除损伤。复制叉恢复：由同源重组（HR）完成双链重建

维持遗传信息的**稳定性**，增加遗传信息的**多样性**。

### 抗体多样性

* 不同的**V D J**片段排列组合
* VDJ重排中片段的加和减
* 不同重链与轻链的配对
* 重链类型转换
* 可变区体细胞高频突变

![Test](img/img-DNA_metabolism/3.png)

## Future

### mini-genome

A single chromosome yeast -- Shao et al (2018) Nature

讨论为什么染色体为什么很多条，分条有什么用？进化考量？分条目的为了有序？

### HAC（Human Artificial Chromosomes）

Synthetic Mini-chromosome -- Glennis A. Logsdon st al (2019) Cell

## Quize

什么是 DNA代谢？描述DNA的化学结构与力学性质



DNA代谢是指细胞内与DNA分子的合成、修复、复制、重排和降解等相关的生物化学过程。它是遗传信息传递和维持基因组完整性的重要基础。DNA代谢包括以下几个主要过程：

​	1.	DNA复制：DNA通过半保留复制的方式进行复制，确保细胞分裂时将遗传信息准确传递给子代细胞。

​	2.	DNA修复：DNA受损时，细胞会通过多种修复机制（如碱基切除修复、核苷酸切除修复等）修复损伤，保持基因组的稳定性。

	3.	DNA重排和重组：在基因重排、染色体重组和交叉等过程中，DNA序列可能发生变化，有助于遗传多样性的产生。
	3.	DNA降解：DNA的降解通常与细胞凋亡、基因表达调控或RNA处理等过程相关。



DNA的化学结构：

DNA（脱氧核糖核酸）是由两条长链核苷酸聚合物组成的双螺旋结构。每个核苷酸由三部分组成：

​	1.	脱氧核糖：由五碳糖（脱氧核糖）构成，它与磷酸基团和碱基相连。

​	2.	磷酸基团：连接两个核苷酸单元，是DNA链的骨架。

​	3.	氮碱基：四种碱基包括腺嘌呤（A）、鸟嘌呤（G）、胸腺嘧啶（T）和胞嘧啶（C），通过氢键相互配对：A与T配对，G与C配对。



两条DNA链通过碱基对之间的氢键连接，形成双螺旋结构。在该结构中，磷酸-脱氧核糖骨架位于外侧，而碱基对位于内侧。



DNA的力学性质：

​	1.	双螺旋结构：DNA的双螺旋结构是由两条互补的链通过碱基配对连接在一起的，每条链按照5’到3’的方向排列。这个结构对DNA的稳定性和复制有重要意义。

​	2.	扭曲和超螺旋：由于DNA链的扭曲，DNA呈现出“超螺旋”结构。这种超螺旋结构是通过拓扑酶（如DNA拓扑异构酶）进行调控的，有助于DNA的紧密包装和解旋。

​	3.	结构动态性：DNA的结构并不是一成不变的，它会根据环境条件、酶的作用或复制和转录的需求发生一定的变形。例如，在转录过程中，DNA需要解旋以便RNA聚合酶能够合成RNA链。

	4.	弹性和柔韧性：DNA分子表现出一定的弹性和柔韧性，使其能够在细胞核中折叠成紧密的染色体结构，同时又能在复制或修复时进行解旋。



环挤压的作用：

1. 压缩
2. 调节基因表达。eg. 增强启动子蛋白相互作用：cohesin 介导的染色质环挤压促进enhancer 和promoter 相互结合。
3. 基因重排。eg. 抗体
4. DNA损伤修复。
