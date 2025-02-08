---
title: RNA
date: 2024-12-18 22:35
categories: BIO-2000-Molecular_biology
tags:
    - "RNA"
    - "RNAi"
    - "course"
excerpt: false
---

## Foundation

### mRNA

#### Type of polymerase

* RNA聚合酶I：5.8、18、28S rRNA gene
* RNA聚合酶II：protein coding genes、mi/ siRNA gene
* RNA聚合酶III：5s rRNA、tRNA

#### Progressing of RNA precursors

真核生物特有转录后修饰，原核生物没有

 **5’加帽**：在RNA聚合酶II转录本上，当RNA转录出15 - 20个核苷酸时，由**鸟苷酸转移酶和甲基转移酶**等作用，在5’端添加m7GpppN帽结构，此过程主要在细胞核中进行，与转录过程偶联。

**剪接**：去除前体mRNA中的内含子，将外显子连接起来。由剪接体（包含多种U snRNPs和辅助蛋白）识别5’剪接位点、分支点（A）和3’剪接位点，通过**两次连续的转酯反应**完成，可产生组成型剪接和可变剪接，可变剪接增加了蛋白质组的多样性。（**非经典剪接产生环状RNA**）

**3’端加工**：在特定信号（如AAUAAA）指导下，由多种蛋白质因子（如CPSF、CstF等）参与，对mRNA前体进行切割并添加poly(A)尾，其长度可调节，影响mRNA的稳定性和翻译效率等。（**Histone mRNA以茎环结构结尾**）

**修饰**：如m6A修饰，由特定的写入蛋白（如METTL3等）添加，可被读取蛋白（如YTHDF2等）识别，影响mRNA的稳定性、翻译效率、出核转运等过程。

**编辑**：包括A to I、C to U等编辑方式，可改变编码区的氨基酸序列或影响mRNA的剪接、出核和翻译等过程（在编码区外）。

#### RNA extranuclear transport

在细胞核中，mRNA转录完成后，经过加工（5’加帽、剪接、3’端加工、修饰等）形成成熟的mRNA，并与多种蛋白质结合形成mRNP复合物。然后，通过核孔复合物（NPC）进行出核转运。出核转运过程中，mRNA的5’帽、3’poly(A)尾等结构以及相关的蛋白质因子（如exportin等）参与识别和运输，将mRNA从细胞核转运到细胞质中，在细胞质中参与蛋白质合成等过程。

* 主要因子
  * **mRNA本身结构相关因子**：5’帽、3’poly(A)尾等结构对mRNA出核转运至关重要。5’帽可促进mRNA出核因子的招募，3’poly(A)尾也参与其中。
  * **核输出受体**：如在高等真核生物中，NXF1/NXT1异二聚体是mRNA出核受体，可识别并结合mRNA，介导其通过核孔复合物出核；在酵母中，Mex67/Mtr2起类似作用。
  * **衔接蛋白**：如TAP/p15等，协助mRNA与核输出受体结合，促进出核过程。
  * **其他相关因子**：如Ran GTPase，通过其循环（RanGTP与RanGDP的转换）为出核转运提供能量并调节转运方向；ALY/Yral等因子也参与其中，促进mRNA的招募和转运。

#### RNA decay

三类主要的RNA 降解酶：内切酶、5’-3’外切酶，3’-5’外切酶

降解途径：无义诱导mRNA讲解、降解无法终止mRNA、降解遇到阻碍mRNA、无加工修饰mRNA

避免降解途径：出核转运、有保护RNA 避免被降解的修饰标签或与特定蛋白结合、有特殊的二级结构、定位于特殊区域，如染色体

### RNAi (RNA interference)

指一种分子生物学上由双链RNA诱发的基因沉默现象，其机制是通过阻碍特定基因的转录或翻译]来抑制基因表达。当细胞中导入与内源性mRNA编码区同源的双链RNA时，该mRNA发生降解而导致基因表达沉默。核RNAi通过影响组蛋白修饰（如H3K9me3和H3K27me3）和抑制转录来实现基因沉默，这种沉默效应可以遗传给后代，这种现象被称为RNA干扰的**跨代遗传现象**。RNAi遗传可分为沉默信号的建立、传递和维持三个过程。

![RNAi](img/img-RNA/1.png)

#### Mechanism

##### siRNA

![siRNA](img/img-RNA/2.jpg)

##### microRNA

Pri-miRNA（初级转录产物）—> Drosha —> pre-miRNA（前体）—> Dicer —> miRNA 

![miRNA](img/img-RNA/3.png)

##### DIfference

1. 起源

   * **siRNA**：通常由双链RNA（dsRNA）通过Dicer酶处理产生，dsRNA可能来自外源性病毒感染、转基因构建或者实验中的人工引入。

   * **miRNA**：由内源性基因编码，通常通过基因转录生成初级miRNA（pri-miRNA），然后通过Drosha酶和Dicer酶加工形成成熟的miRNA。
2. 功能
   * **siRNA**：主要用于通过靶向特定mRNA分解来抑制基因表达。这种过程通常通过RISC（RNA诱导沉默复合物）完成，siRNA会与靶mRNA完全配对，引导mRNA降解。
   * **miRNA**：主要通过部分配对的方式与靶mRNA结合，通常抑制翻译或者导致mRNA的稳定性降低。miRNA的靶标通常是多个，不同的mRNA可能共享相同的miRNA靶序列。

3. 靶标识别
   * **siRNA**：通常具有高特异性，能够与靶mRNA完全配对。
   * **miRNA**：由于部分配对，靶标的选择较为宽泛，一条miRNA可能调控多个靶基因。

4. 长度
   * **siRNA**：长度一般为21-23个核苷酸。
   * **miRNA**：通常也为21-23个核苷酸，但成熟miRNA的前体（pri-miRNA）较长。

5. 表达模式
   * **siRNA**：通常是外源性引入的，主要在实验中用来沉默特定基因，或者在病毒感染等应答中
   * **miRNA**：作为内源性调控因子，在细胞正常生理过程中表达，参与多种生物学过程，如发育、细胞周期调控、免疫反应等。
