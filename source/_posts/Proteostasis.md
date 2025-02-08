---
title: Proteostasis
date: 2024-12-16 14:18
categories: BIO-2000-Molecular_biology
tags:
    - "Protein"
    - "Proteostasis"
    - "course"
    - "Ubiquitin modification"
excerpt: false
---

## Foundation

### Ubiquitin

* Highly conserved in all eukaryotes

* 大约70个氨基酸组成，本身7个氨基酸可以被泛素化修饰

* ~ 1 -2% total proteins in the cell

* Ubhomoestasisis up to constant change

* Very dynamic：ubiquitylation vs de-ubiquitination

![ups](img/img-Proteostasis/2.png)

### Ubiquitin-proteasome system (UPS)

![ups](img/img-Proteostasis/1.png)

*  E1酶（泛素活化酶，Ubiquitin-activating enzyme）
  * E1酶通过消耗ATP，将泛素分子的C末端（Gly76）的羧基与自身的半胱氨酸（Cys）残基形成硫酯键。
  * 激活的泛素随后被转移到E2酶上。
*  E2酶（泛素结合酶，Ubiquitin-conjugating enzyme）
  * 将泛素从E1转移到自身的活性位点（半胱氨酸上），然后进一步转移到目标蛋白（在E3酶的辅助下）。
*  E3酶（泛素连接酶，Ubiquitin ligase）
  * 决定泛素化的特异性，通过识别目标蛋白，并协助E2酶将泛素连接到目标蛋白的赖氨酸残基上。

### Ubiquitin Signaling

Ubiquitin Codes

* coding by specific

  * E3连接酶有两种方式添加泛素蛋白：
    * “Hug”模式：E3上面既结合了E2也结合了底物，E2泛素结合酶直接把泛素加到底物上面。E3没有直接接触到Ub，只是在中间起到了一个空间骨架的作用，拉近了E2 和底物之间的距离
    * “Kiss”模式：E3 上面既结合了E2 也结合了底物，E2把泛素传递给 E3上的特殊位点，经常是基然后形成硫酯键，过后再传递给底物
  * Ub在底物上可以结合多个位点，单泛素化；或单个位点结合多个（poly）泛素化

* Edition by DUBs and PTMs

  * 泛素 code 的时候也会对其进行编辑，用DUB（去泛素化酶）、PTM（如磷酸化等）等

    方式进行编辑，比如 Ser65 磷酸化对 Parkin 蛋白功能会有很多影响。

  * 例子：泛素的65位丝氨酸经过激酶 PINK1 蛋白催化磷酸化后不能与 UBD、E3 等蛋白作用了。但它可以激活 parkin（是一种含ring 结构域的E3连接酶），本来处于自我抑制的关闭状态不能结合 E2 连接酶，但在它结合 65 位磷酸化的 Ub 后被激活，这个信号通路在线粒体自噬中起作用，它被激活后使得一系列的受体蛋白识别产生自噬体包围线粒体出现线粒体自噬。

* Decoding by UBDs（泛素结合结构域）

  * UBD 和Ub 之间有很多种作用方式，Mono-Ub 被 UBD 结合蛋白识别通过Ub44 位异亮氨酸，Ub 和UBD 之间多种共价相互作用增加特异性和亲和力，Decodet-即 UBD，不同的UBD 识别不同的泛素化修饰进而产生不同的生理学功能。
  * 泛素结合蛋白（UBP）与泛素化蛋白结合，阻止泛素化

泛素信号通过E3连接酶的作用生成，随后可以被DUB或PTM修饰以进一步调控功能；UBD对泛素化修饰的解码则赋予其生物学意义。这些机制广泛参与蛋白降解、信号传递、细胞周期调控及细胞应激反应等多个重要生物学过程。

### Ubiquitin homeostasis

泛素合成、降解，聚泛素链组装和拆卸的过程。泛素化和去泛素化是⼀个动态平衡过程。

泛素应激——Ub stress 

* 泛素减少：减数分裂缺陷、组织⽣长缺陷、增殖缺陷、扰乱造⾎系统、神经退化和代谢紊乱、细胞分化异常、改变药物应答； 
* 泛素增加：延迟衰⽼、改变基因表达、促进细胞增殖和应急耐受、维持肿瘤细胞特性、改变蛋⽩酶体构成、激活⾃噬 

N端规则：每一种蛋白质都有寿命特征，称为半衰期(half-life)。蛋白质的半衰期与多肽链 N-端特异的氨基酸有关，它们对蛋白质的寿命有控制作用。蛋白质 N-末端与半衰期的关系，称为 N 端规则。如末端是精氨酸、赖氨酸、天冬氨酸或谷氨酸等的多肽，寿命就很短，因为如 Arg 这样 N 端带有疏水性或带正电的氨基酸的蛋白更容易被泛素化，从而容易被降解。而如 Asp、Glu 被氧化后会带上 Arg，也容易发生泛素化被降解；而末端是缬氨酸或甲硫氨酸的多肽,寿命就很长。
