---
title: Hardy-Weinberg Equilibrium (HWE)
date: 2025-02-11 16:08
categories: Heredity and evolution
tags:
    - "course"
    - "Hardy-Weinberg"
excerpt: false
---

遗传概括：基因型 --> 表型，而表型在选择压力后反过来影响基因型，造就了基因型的选择

### Concept

* 突变（mutation）。一般认为稀有变异小于1%称为突变
* 遗传多态性（genetic polymorphism）。稀有突变频率大于百分之1称为遗传多态
* 遗传座位（locus）
* 等位基因（allele）
* 核苷酸位点（nucleotide）
* 序列（sequence）
* 位点（site）
* 分离位点（segregating site）
* 单倍体（haploid）、二倍体（diploid）
* 基因型（genotype）
* 杂合子（heterozygote）、纯合子（homozygotye）
* 等位基因频率（allele frequency）
* 基因型频率（genotype frequency）

{% notel default fa-info note %}

二元性SNV（Single Nucleotide Variant）

{% endnotel %}

例子：

- 原始序列：`A`
- 变异序列：`G`
- 该位置只有`A`和`G`两种可能，因此是二元性SNV。为什么？考虑突变的概率，通常这个数值被认为是$$10^{-7}$$左右的概率，考虑人类存在的时间导致G二次突变为其他的概率不满足。注意不能搞乱 1. 突变过程本身是随机的，A可能变成C、G、T。 2. 二元性SNV是对实际数据（如群体或个体中观察到的变异）的简化描述，仅记录两种主要类型。

### Hardy-Weinberg Equilibrium (HWE)

**群体中的等位基因频率以及基因型频率并不随世代的推移而变化。**

#### Demonstrate

一个群体由N个个体组成，其中有一对常染色体等位基因A, a，其频率分别以p、q表示。可能的基因型为AA（n1），Aa（n2），aa（n3）三种，其频率分别以D（n1/N）、H（n2/N）、R（n3/N）表示，其中D+H+R=1。

$$p=\frac {2n1+n2} {2N}=D+\frac{H}{2},q=\frac {2n3+n2} {2N}=R+\frac{H}{2}$$

亲本的配子（子一代）基因型概率

|                | 卵 A (p) | 卵 a (q) |
| -------------- | -------- | -------- |
| **精子 A (p)** | AA (p²)  | Aa (pq)  |
| **精子 a (q)** | Aa (pq)  | aa (q²)  |

子一代向下一代提供的配子中两种基因频率分别是

$$A=p^2+\frac{1}{2}(2pq)=p^2+pq=p(p+q)=p,a=q^2+\frac{1}{2}(2pq)=q^2+pq=q(p+q)=q$$

基因型的频率未发生改变

#### Basic condition

1. Random mating

2. No differential fertility（生育能力） of the genotypes

3. Equal genotype frequencies in the two sexes

4. No mutation

5. No immigration(移民)

6. No differential emigration

7. No differential viabilit

8. **Infinite population size**

而打破条件，造成的不平衡动力元素：突变(mutation)，婚配(random mating) /重组(recombination)，选择(selection)，漂变(drift)，迁移(migration)

因此对于一个特定的地理群体，绝大部分基因组处于HWE状态。

#### Conclusion

* Aa×Aa的交配频率永远为AA×aa交配频率的2倍,因此aa在群体中不易消失，总保持一定频率。当一般群体中隐性基因个体稀少的时候，大多数aa是Aa的后代。
  * Aa × Aa 的交配需两个杂合体同时存在，其频率是$$ (2pq)^2=4p^2q^2$$
  * AA × aa 的交配需显性纯合体和隐性纯合体同时存在（雌雄不同区分），其频率是 $$2（p^2\times q^2）=2p^2q^2$$。
  * 例子，一个隐形性状发病概率$$q^2(aa)=\frac{1}{10000}$$

| **产生隐性后代的亲本组合** | **Aa × Aa**               | **Aa × aa**               | **aa × aa**            | **总计** |
| :------------------------- | ------------------------- | ------------------------- | ---------------------- | -------- |
| **在所有交配中**           | $$p^2q^2 $$               | $$2pq^3$$                 | $$q^4$$                | $$q^4$$  |
| **在产生 aa 后代的交配中** | $$\frac{p²q²}{q²} = p² $$ | $$\frac{2pq³}{q²} = 2pq$$ | $$\frac{q⁴}{q²} = q²$$ | 1        |

* 当q很小时，p=1，则H-W’s law取得一种极限形式。差不多所有的隐性基因都处于杂合状态中，杂合子个体的比例约为隐性基因频率的两倍。（aa=$$q^2$$，AA=1-2q，**Aa=2q**），发病概率为$$q^2$$,	杂合子频率$$=2\sqrt{q(发病率)}$$。案例，55,715个婴儿中有5例为该病患者，隐形基因频率$$q=\sqrt{\frac{5}{55715}}=0.0095$$，但是正常人携带频率$$2\sqrt{0.0095}=0.195$$,高达百分之2的携带率
* 计算等位基因频率（隐性）。例子：某种常染色体隐性遗传病（白化病）在一特定人群中频率，就能计算这个异常基因的携带者和基因频率。白化病发病（aa）($$q^2$$)的频率为1／10000，杂合子携带者的频率为$$2pq=2\times99／100\times1／100≈1／50$$​。在比例中，每个受累的个体将有200个左右在临床上无症状的携带者。
* 计算等位基因频率（显性）。常染色体显性遗传病，如并指症，在一个群体多为杂合子（Aa）发病。杂合子（H）的频率为2pq，由于q值大，近于1，故H＝2p,p=1/2H。并指症的发病率为1／1000，H＝1／1000，p=1/2H=1/2000,即致病基因A的频率为0.05%
* 罕见的X染色体连锁隐性遗传病。**女性患病率是男性患病率的2倍**
* 常染色体隐性遗传病。杂合携带者频率约为致病基因频率的**2**倍

### HWE的偏离（固定指数）

当实际观察到的基因型频率与HWE预期值不符时，称为HWE的偏离。 F 是固定指数，反映了基因型频率与Hardy-Weinberg预期的偏离程度。 (1 - F) 代表没有偏离Hardy-Weinberg平衡的部分。引入 $F$ 是因为近交导致了等位基因的来源不再是完全随机的，而是更可能来自同一祖先。因此，当有近交时，相同等位基因的配对更为频繁，这影响了基因型的频率。

* $$X_{11}$$ 是纯合基因型 A/A 的频率，其期望频率为$$ x_1^2$$ 。偏离后：$$X_{11} = (1 - F) x_1^2 + F x_1 $$。（	**$(1 - F) x_1^2$** 代表没有近交时的频率，仍然符合HWE预期。**$F x_1$** 表示由于近交而使得纯合基因型 A/A 的频率增高的部分）
* $$X_{12}$$ 是杂合基因型 A/a 的频率，其期望频率为 $$2x_1 x_2$$ 。偏离后：$$ X_{12} = 2(1 - F) x_1 x_2$$。（由于近交会增加纯合基因型（A/A 或 a/a）的比例，杂合基因型 A/a 会减少。）
* $$X_{22}$$ 是纯合基因型 a/a 的频率，其期望频率为$$ x_2^2$$ 。偏离后：$$X_{22} = (1 - F) x_2^2 + F x_2 $$

最终得到$$F = \frac{2x_1 x_2 - X_{12}}{2 x_1 x_2}$$.（通过已知的基因型频率$$ X_{12} $$和等位基因频率$$ x_1$$ 和$$ x_2$$ 来计算偏离的程度，从而得出固定指数 F ）

如果 $F = 0$，则群体完全符合HWE，基因型频率与期望一致；如果 $F > 0$，则群体存在近交，基因型频率会偏离预期。

### Sub-population

大多数的自然群体可被再分为许多不同的繁殖单位或亚群体（sub-population），尽管这些群体并不是完全隔离的。**$x_k$** 表示第 $k$ 个亚群体中，等位基因 **$A_1$** 的频率。显然，在每个亚群体内部，等位基因频率 $x_k$ 和 $1 - x_k$ 分别代表 **$A_1$** 和 **$A_2$​** 等位基因的频率。**$w_k$** 表示第 $k$ 个亚群体的相对大小。相对大小的总和为1，即$$\sum_{k=1}^{s} w_k = 1$$

* $$P(A_1A_1) = \sum_{k=1}^{s} w_k x_k^2 =1 X_{11} = \overline{x}^2 + \sigma^2$$
* $$P(A_1A_2) = \sum_{k=1}^{s} w_k \cdot 2x_k(1 - x_k) = X_{12} = 2\overline{x}(1 - \overline{x}) - 2\sigma^2$$
* $$P(A_2A_2) = \sum_{k=1}^{s} w_k \cdot (1 - x_k)^2 = X_{22} = (1 - \overline{x})^2 + \sigma^2$$

$$ \sigma^2 = \sum_{k=1}^{S} w_k (x_k - \overline{x})^2 $$是群体中等位基因频率的方差

$$\overline{x} = \sum_{k=1}^{S} w_k x_k $$是群体中 等位基因的平均频率

在与单群体的公式对比，得到了$$F = \frac{\sigma^2}{[\overline{x}(1-\overline{x})]}$$

**表明如果一个群体被分为多个交配单位，纯合子的频率要高于Hardy-Weinberg比率。**带来了对于杂种优势、自然选择的启示

### HWE的常见检测

#### $$X^2$$-test

$$X^2=\sum\frac{(O-E)}{E}$$,observe ，expect value

#### 精确检验

$$\Pr(N_{AB} = n_{AB} \mid N, n_A) = \frac{2^{n_{AB}} \cdot N! \cdot n_A! \cdot n_B!}{n_{AA}! \cdot n_{AB}! \cdot n_{BB}! \cdot (2N)!}$$

#### 应用

* 数据分析中，检测可能的数据质量问题（typing error）。– Case-control study 一般要求所有检测位点在control中处于HWE。
* 多个位点处于HWD暗示近亲婚配或群体结构的存在。
* 在排除其他可能的因素以后，筛选可能受到自然选择的基因。

| Observation of HWD      | Interpretation                                    |
| ----------------------- | ------------------------------------------------- |
| A lot of random markers | Population structure or a bad data set            |
| A few adjacent markers  | Probably natural selection or disease association |
| Sporadic markers        | Genotyping or Sequencing error                    |

#### HWE的多重检验

多重检验是统计分析中的一个重要问题，尤其是在基因组学等领域，通常需要同时检验成千上万的假设。多重检验的问题当进行大量统计检验时，获得假阳性（Type I 错误）的概率会增加。在多重检验中，若直接使用原始p值进行推断，假阳性（第一类错误）的概率会显著增加。这是因为**原始的显著性水平（α）是针对单个检验设计的**，而多重检验会大幅提高整体犯错的概率。例如：

- 如果你用 p 值阈值 0.05 检验 10,000 个基因，即使没有真正的关联，也可能有 500 个基因（10,000 的 5%）纯粹由于随机因素而被认为是显著的。

常见的多重检验校正方法的简要说明，包括 **Bonferroni 校正**、**Bonferroni Step-down (Holm) 校正**、**Westfall and Young 置换法** 以及 **Benjamini and Hochberg 错误发现率（FDR）**得到p-value

| 方法                            | 控制目标 | 优点                           | 缺点                               |
| :------------------------------ | :------- | :----------------------------- | :--------------------------------- |
| **Bonferroni 校正**             | FWER     | 简单，严格控制假阳性           | 过于保守，假阴性率高               |
| **Bonferroni Step-down (Holm)** | FWER     | 比 Bonferroni 更灵活，功效更高 | 依然相对保守                       |
| **Westfall and Young 置换法**   | FWER     | 考虑检验相关性，适用于复杂数据 | 计算复杂度高                       |
| **Benjamini and Hochberg FDR**  | FDR      | 宽松，适用于大规模数据分析     | 控制的是假阳性比例，可能仍有假阳性 |

