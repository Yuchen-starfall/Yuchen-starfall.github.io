---
title: Organelle assemble
date: 2024-12-15 19:33
categories: Genomics
tags:
    - "Assemble"
excerpt: false
---

## Purpose

由于NGS技术短读长的特点，在面对拥有这大量长片段的重复序列的线粒体基因组时，使用二代测序/二代三代测序数据混装的细胞器基因组的效果不佳。三代测序发展的今天，尝试重新组装线粒体基因组。最终目的是**使用最少的reads**去组装出一个**与参考基因组覆盖度最高**的细胞器基因组。

![mt_genome](img/img-organelle_assemble/1.png)

## Technical route

![technical_route](/img/img-organelle_assemble/2.png)

## Process

### Filter contig from genome

#### Purpose

已有，预组装的基因组.fa文件。将高通量HiFi测序reads 组装为contig。将预组装基因组文件与参考基因组比对，筛选出大于80%的contig，将筛选出的contig放入一个文件，为下一步做准备。

#### Software

##### MUMmer

`MUMmer`中的`nucmer`用于对多 Fasta 数据文件中包含的核苷酸序列进行全部与全部比较。它最适合用于可能具有大量重排的相似序列。`promer`用于蛋白质水平，核苷酸输入文件在所有 6 个阅读框架中翻译，然后通过与 nucmer 相同的方法相互对齐。

`nucmer [options] <reference> <query>`

* -p：指定输出文件前缀
* --delta=PATH：指定 .delta 文件的输出路径
* --mum：使用在参考序列和查询序列中都唯一的锚点进行比对
* --maxmatch：使用所有的锚点进行比对，而不考虑唯一性

`show-coords -r -T <out.delta>`

```
<reference geneme location> <query genome location>
NUCMER

[S1]    [E1]    [S2]    [E2]    [LEN 1] [LEN 2] [% IDY] [LEN R] [LEN Q] [COV R] [COV Q] [TAGS]
31099   60341   273647  244407  29243   29241   99.88   222059  490520  13.17   5.96    ptg000001l      BA000029.3
60334   70901   195395  184828  10568   10568   100.00  222059  490520  4.76    2.15    ptg000001l      BA000029.3
70905   85506   184860  170251  14602   14610   99.86   222059  490520  6.58    2.98    ptg000001l      BA000029.3
85499   95965   41369   51835   10467   10467   99.50   222059  490520  4.71    2.13    ptg000001l      BA000029.3
85499   90763   135896  141160  5265    5265    99.98   222059  490520  2.37    1.07    ptg000001l      BA000029.3
```

```txt
[S1]    Start of the alignment region in the reference sequence.

[E1]    End of the alignment region in the reference sequence.

[S2]    Start of the alignment region in the query sequence.

[E2]    End of the alignment region in the query sequence.

[LEN 1] Length of the alignment region in the reference sequence,measured in nucleotides.

[LEN 2] Length of the alignment region in the query sequence, measured in nucleotides.

[% IDY] Percent identity of the alignment, calculated as the(number of exact matches) / ([LEN 1] + insertions in the query).

[% SIM] Percent similarity of the alignment, calculated like the above value, but counting positive BLOSUM matrix scores instead of exact matches.

[% STP] Percent of stop codons of the alignment, calculated as(number of stop codons) / (([LEN 1] + insertions in the query) * 2).

[LEN R] Length of the reference sequence.

[LEN Q] Length of the query sequence.

[COV R] Percent coverage of the alignment on the reference sequence, calculated as [LEN 1] / [LEN R].

[COV Q] Percent coverage of the alignment on the query sequence, calculated as [LEN 2] / [LEN Q].

[FRM]   Reading frame for the reference sequence and the reading frame for the query sequence respectively.  This is one of the columns absent from the nucmer data, however, match direction can easily be determined by the start and end coordinates.

[TAGS]  The reference FastA ID and the query FastA ID.
```

##### seqtk

seqtk 是一个使用C语言编写的轻量级的工具集，专门用于处理 FASTA 和 FASTQ 格式的生物序列数据。它非常适合用于大规模基因组数据的处理，能够高效地处理和转换序列数据。

1. **提取子序列：** 从 FASTA/FASTQ 文件中提取特定的序列（例如基于 ID 提取 reads）。

```
seqtk subseq input.fastq reads_ids.txt > output.fastq
```

2. **格式转换：** 转换序列文件的格式，例如从 FASTQ 转为 FASTA，或者反向转换。

```
seqtk seq -a input.fastq > output.fasta
```

3. **抽样：** 从大数据集中随机抽取子集（比如抽取部分 数量reads 进行分析）。

```
seqtk sample input.fastq 1000 > sample.fastq
```

4. **质量控制：** 剔除低质量的序列或 reads。保留平均质量值大于等于 20 的 reads，质量值是根据 ASCII 码计算

```
seqtk seq -q 20 input.fastq > filtered.fastq
```

5. **合并文件：** 将多个 FASTA/FASTQ 文件合并为一个。

```
seqtk seq -A file1.fasta file2.fasta file3.fasta > merged.fasta
seqtk seq -q 20 file1.fastq file2.fastq file3.fastq > merged.fastq
```

#### Pipeline

```bash
nucmer -p <output name> <reference genome> <query genome>
```

```bash
 show-coords -r -T -l -c <out.delta> | sort -k12,12 -k1,1n > <filter.txt>
```

* -r：对输出的比对结果按参考序列的坐标**升序**排序。（默认情况下，比对结果是按照输入顺序输出的）
* -T：启用制表符分隔输出（Tab-delimited output）。（默认的输出是用空格对齐的文本格式，阅读起来比较直观，但不便于程序解析）
* -l：包含序列长度信息 -- LEN R和LEN Q
* -c ：包含覆盖度信息 -- COV R和COV Q

`sort -k12,12 -k1,1n `这个命令会根据两个排序条件来排序文件：

1. **按第12列排序**：-k12,12 指定首先按第9列（字段）进行排序，这是主要的排序条件。
2. **按第1列进行数字排序**：-k1,1n 指定在第9列排序后，对于第1列（字段）进行数字排序（n 表示按数字大小排序，而不是按字母顺序）。

统计每条contig的覆盖度

{% notel blue 提示 %}
简单的累加同一条contig中的COV R或COV Q的值，特别是在同一 contig 上有多个匹配段且这些段之间存在重叠的情况下，重复计算这些重叠区域会导致覆盖度被高估。
{% endnotel %}

 `python <coberage.py> <input.txt> <output.txt> `

```python
import re
import argparse
from collections import defaultdict

# 定义函数：合并区间
def merge_intervals(intervals):
    if not intervals:
        return []
    # 按起点排序
    intervals.sort()
    merged = [intervals[0]]
    for current in intervals[1:]:
        prev_start, prev_end = merged[-1]
        curr_start, curr_end = current
        if curr_start <= prev_end:  # 存在重叠
            merged[-1] = (prev_start, max(prev_end, curr_end))  # 合并区间
        else:
            merged.append(current)  # 新的区间
    return merged

# 读取输入文件
def parse_file(file_path):
    contig_intervals = defaultdict(list)  # 用于存储每个参考序列的比对区间
    contig_lengths = {}  # 用于存储每个参考序列的总长度 (LEN R)

    with open(file_path, 'r') as file:
             # 跳过前四行 -- delta格式决定
        for _ in range(4):
            next(file)
        for line in file:
            # 跳过表头或空行
            if line.strip() == "" or re.match(r"^\[S1\]", line):
                continue
            
            # 按制表符分割每一行
            cols = line.strip().split('\t')
            start, end = int(cols[0]), int(cols[1])  # S1, E1
            contig = cols[11]  # TAGS 中的参考序列名称
            length_r = int(cols[7])  # LEN R
            
            # 添加区间到对应参考序列
            contig_intervals[contig].append((start, end))
            # 记录参考序列的总长度
            contig_lengths[contig] = length_r

    return contig_intervals, contig_lengths

# 计算覆盖度
def calculate_coverage(contig_intervals, contig_lengths):
    coverage_results = {}
    for contig, intervals in contig_intervals.items():
        merged_intervals = merge_intervals(intervals)
        total_coverage = sum(end - start + 1 for start, end in merged_intervals)
        reference_length = contig_lengths[contig]
        coverage_percentage = (total_coverage / reference_length) * 100
        coverage_results[contig] = (total_coverage, coverage_percentage)
    return coverage_results

# 主程序
def main():
    # 设置命令行参数解析
    parser = argparse.ArgumentParser(description="Calculate the coverage of reference sequences based on nucmer output.")
    parser.add_argument("input_file", help="Path to the input txt file containing nucmer coordinates.")
    parser.add_argument("output_file", help="Path to the output file where results will be saved.")
    
    args = parser.parse_args()
    
    # 解析输入文件
    contig_intervals, contig_lengths = parse_file(args.input_file)
    
    # 计算覆盖度
    coverage_results = calculate_coverage(contig_intervals, contig_lengths)
    
    # 将结果保存到输出文件
    with open(args.output_file, 'w') as output_file:
        output_file.write(f"{'Contig':<20} {'Total Coverage':<15} {'Coverage (%)':<15}\n")
        for contig, (total_coverage, coverage_percentage) in coverage_results.items():
            output_file.write(f"{contig:<20} {total_coverage:<15} {coverage_percentage:.2f}\n")
    
    print(f"Results have been written to {args.output_file}")

# 执行脚本
if __name__ == "__main__":
    main()
```

最终的输出如下

```txt
Contig               Total Coverage  Coverage (%)
ptg000001l           152557          68.70
ptg000002l           69997           86.49
ptg000003l           38846           51.78
ptg000004l           120567          82.39
ptg000005l           46787           100.00
```

筛选出大于80的contig ID

```
awk 'NR > 1 && $2 >= 80 {print $1}' <input.txt> > <output_ID.txt>
```

根据ID提取序列

```
seqtk subseq <input.fastq> <contig_ids.txt> > <extracted_contig.fastq>
```

### Filter HiFi reads

#### Purpose

将上一步得到的与参考基因组覆盖度大于80%的contig 整合在一起，与高通量测序比对，筛选出高覆盖度的reads，将reads提取出来，为后续的再组装做准备。

#### Software

##### bedtools

专门设计用于处理基因组数据，特别是基因组区域之间的交互、统计和分析。它支持多种常见的生物学数据格式，如 BED、GFF、VCF、BAM、SAM 等。bedtools 的核心功能包括对基因组区域的操作、格式转换、统计计算以及文件间的交互。

* 寻找交集：`bedtools intersect -a file1.bed -b file2.bed`
* 合并：`bedtools merge -i file.bed`
* 计算覆盖度：`bedtools coverage -a regions.bed -b reads.bam`
* 排序：`bedtools sort -i file.bed`
* BED文件转换为BAM：`bedtools bedtobam -i input.bed -g genome.txt > output.bam`
* BAM文件转换为FASTQ格式：`bedtools bamtofastq -i input.bam -fq output.fastq`

BED格式文件

| **字段**    | **描述**                                    | **必选** |
| ----------- | ------------------------------------------- | -------- |
| chrom       | 染色体名称或序列标识符                      | 是       |
| chromStart  | 区域的起始位置（0-based）                   | 是       |
| chromEnd    | 区域的结束位置（不包含chromEnd位置）        | 是       |
| name        | 区域的名称或标识符（可选）                  | 否       |
| score       | 区域的得分（通常是0到1000之间的整数，可选） | 否       |
| strand      | 区域所在的链（+ 或 -，可选）                | 否       |
| thickStart  | 编码区域的起始位置（可选）                  | 否       |
| thickEnd    | 编码区域的结束位置（可选）                  | 否       |
| itemRgb     | RGB颜色值（可选）                           | 否       |
| blockCount  | 区域的块数（可选）                          | 否       |
| blockSizes  | 块的大小列表（可选）                        | 否       |
| blockStarts | 块的起始位置列表（可选）                    | 否       |

##### Minimap2

高效的序列比对工具，主要用于大规模基因组数据比对和长读（long-read）数据的对齐。它广泛应用于基因组学、转录组学、变异检测等领域，特别适合处理高通量测序数据，如短读（short-read）和长读（long-read）的比对。minimap2 的设计初衷是提供更快速、更准确的比对算法，特别适用于大规模基因组比对任务。

* -x [preset]
  * -x map-ont：Oxford Nanopore 长读比对。
  * -x map-pb：PacBio 长读比对。
  * -x sr：短读比对（单端和双端）。
  * -x splice：带有剪接信息的 RNA-seq 比对。
  * -x map-hifi：PacBio HiFi/CCS 比对
* -a 生成 SAM 格式的比对结果（标准输出格式）
* -t [num] 指定使用的线程数，默认使用 1 个线程。增加线程数可以加快比对速度
* -p [threshold] 设置比对的最小比对质量阈值，值越大，输出的比对结果越严格
* 查找长读的重叠
  * PacBio：`minimap2 -x ava-pb reads.fq reads.fq > ovlp.paf`
  * Oxford Nanopore：`minimap2 -x ava-ont reads.fq reads.fq > ovlp.paf`

##### BAM文件

BAM是目前基因数据分析中最通用的比对数据存储格式，它既适合于短read也适合于长read，最长可以支持128Mbp的超大read！BAM的纯文本格式（.sam）

查看BAM文件。不建议用VIM，会爆掉

```
less -SN in.sam          # 打开sam文件
samtools view -h in.bam  # 打开bam文件
```

BAM文件分为两个部分：header（@符号打头）和record（有时候也叫alignment section，即，**比对信息**）。这是我们通常所说的序列比对内容，**每一行都是一条read比对信息**

| 字段名 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| QNAME  | 查询名称（Query name），读取的名称或 ID（标识符），用于区分不同的读取。 |
| FLAG   | 标志（Flag），16 位整数，表示多种比对状态（如单端/双端比对、反向比对等）。 |
| RNAME  | 参考序列名称（Reference Name），比对到的参考基因组或染色体的名称。 |
| POS    | 比对位置（Position），1-based，表示比对开始的位置。          |
| MAPQ   | 比对质量（Mapping Quality），一个整数，表示比对结果的可靠性。 |
| CIGAR  | 比对操作符（CIGAR），描述查询序列和参考基因组序列的匹配、插入、缺失等操作。 |
| RNEXT  | 下一个比对的参考序列名称（Reference Name of Next Read），双端比对时表示另一端的参考序列名称。 |
| PNEXT  | 下一个比对的位置（Position of Next Read），双端比对时表示另一端比对在参考基因组上的位置。 |
| TLEN   | 模板长度（Template Length），表示该读取的模板长度，即双端之间的距离。 |
| SEQ    | 序列（Sequence），表示该读取的碱基序列。                     |
| QUAL   | 序列质量分数（Quality Scores），每个碱基的质量分数，通常使用 Phred 质量分数来表示。 |

###### FLAG

**FLAG**信息很重要 -- **反应reads比对信息**

想要读懂它的一个关键点是我们**不能够将其视为一个数字**，而是**必须将其转换为一串由0和1组成的二进制码**，这一串二进制数中的每一个位(注意是“位”，bit的意思)都代表了一个特定信息，它一共有12位（以前只有8位），所以一般会用一个16位的整数来代表，这个整数的值就是12个0和1的组合计算得来的，因此它的数值范围是0~2048

| 标志位 | 二进制位 | 十六进制     | 解释                                                         |
| ------ | -------- | ------------ | ------------------------------------------------------------ |
| 1      | 0x1      | 0000001      | 模板有多个片段（template having multiple segments）          |
| 2      | 0x2      | 0000010      | 每个片段都已正确对齐（each segment properly aligned）        |
| 4      | 0x4      | 0000100      | 片段未对齐（segment unmapped）                               |
| 8      | 0x8      | 0001000      | 下一个片段未对齐（next segment in the template unmapped）    |
| 16     | 0x10     | 0010000      | 序列反向互补（SEQ being reverse complemented）               |
| 32     | 0x20     | 0100000      | 下一个片段的序列是反向互补（SEQ of next segment reverse complemented） |
| 64     | 0x40     | 1000000      | 该片段是模板中的第一个片段（first segment in the template）  |
| 128    | 0x80     | 10000000     | 该片段是模板中的最后一个片段（last segment in the template） |
| 256    | 0x100    | 100000000    | 次级比对（secondary alignment）                              |
| 512    | 0x200    | 1000000000   | 不通过质量过滤器（not passing filters）                      |
| 1024   | 0x400    | 10000000000  | PCR 或光学重复（PCR or optical duplicate）                   |
| 2048   | 0x800    | 100000000000 | 补充比对（supplementary alignment）                          |

so 为看到一个序列的FLAG值为77。则77 = 000001001101 = 1 + 4 + 8 +64。因此得到这个这个FLAG包含的信息在一个由多个片段组成的模板序列中，**第一个片段**和**最后一个片段**可能会面临对齐失败的问题，其中不仅可能有某些片段没有成功比对到参考基因组，甚至可能是**紧接着的下一个片段**也会遇到对齐的问题。因此如果是0则代表完美匹配，没有附加任何额外的标志。

**我们要获得其中某个位（假设第N位）的值——只需要将这个FLAG值和2的N次方做与的运算即可**。在与运算时，FLAG值首先会被转换成一串二进制序列（如77=000001001101），而2的N次方除了第N位是1之外，其它的都是0，“与”了之后其它信息就会被屏蔽掉。比如，我们想知道该read是否比对上了参考序列，那么只需要计算FLAG & 4 的值就行了，如果结果是1那么就是比对上了，如果是0则代表没有比上。假设我们想查看某个序列是否比对上了参考基因组。这个信息通常由FLAG值的第3位表示。在FLAG值的二进制表示中，第3位对应的是4，所以如果我们想知道序列是否比对成功，可以通过以下步骤：

* 将FLAG值（比如77）和4做**与运算**。
* FLAG = 77 的二进制是 000001001101，4 的二进制是 000000000100。
* 77 & 4 = 000001001101 & 000000000100 = 000000000100，结果是 4（不为零）。

如果结果不是零，说明该序列成功比对上了参考基因组。如果与运算结果是零，说明没有比对上。

###### CIGAR

CIGAR是`C`ompact`I`diosyncratic`G`apped`A`lignment`R`eport的首字母缩写，称为“雪茄”字符串。
**作为一个字符串，它用数字和几个字符的组合形象记录了read比对到参考序列上的细节情况，读起来要比FLAG直观友好许多，只是记录的是不同的信息。**

| Op   | BAM  | Description                                           | Consumes Query | Consumes Reference |
| ---- | ---- | ----------------------------------------------------- | -------------- | ------------------ |
| M    | 0    | alignment match (can be a sequence match or mismatch) | yes            | yes                |
| I    | 1    | insertion to the reference                            | yes            | no                 |
| D    | 2    | deletion from the reference                           | no             | yes                |
| N    | 3    | skipped region from the reference                     | no             | yes                |
| S    | 4    | soft clipping (clipped sequences present in SEQ)      | yes            | no                 |
| H    | 5    | hard clipping (clipped sequences NOT present in SEQ)  | no             | no                 |
| P    | 6    | padding (silent deletion from padded reference)       | no             | no                 |
| =    | 7    | sequence match                                        | yes            | yes                |
| X    | 8    | sequence mismatch                                     | yes            | yes                |

###### MAPQ

MAPQ，比对质量值

它告诉我们的是这个read比对到参考序列上这个位置的可靠程度，用错误比对到该位置的概率值（转化为Phred scale）来描述：
$$
\text{MAPQ} = -10 \times \log_{10}(P)
$$
因此MAPQ（mapping quality）值大于30就意味着错比概率低于0.001（千分之一），这个值也是我们衡量read比对质量的一个重要因子。

#### Pipeline

hifi测序文件从bam，转化为fastq。

```
bedtools bamtofastq -i <hifi.bam> -fq <hifi_reads.fastq>
```

使用筛选出的contig与hifi reads进行比对

```
minimap2 -ax map-hifi <extracted_contig.fastq> <hifi_reads.fastq> > <reads.sam>
```

简单查看sam文件

```
samtools view -h <reads.sam> | head
```

筛选出精确比对上的 -- Flag=0

```
awk '{if($2==0)print}' <reads.sam> > <filter_reads.sam>
```

统计出来每条redas比对上的碱基数与覆盖率 -- 即M的数量

```python
import re
import sys

def process_line(line):

    if line.strip() != "" and not line.startswith("#"):

        parts = line.strip().split()
        name = parts[0]
        cigar = parts[5]
        seq = parts[9]

        numbers_before_m = re.findall(r'(\d+)(?=M)', cigar)
        sum1 = sum(int(num) for num in numbers_before_m)
        sum2 = len(seq)

        ratio = sum1/sum2 if sum != 0 else 0
        return name, ratio

def process_file(inputfile, outfile1):
    with open(inputfile, 'r') as infile, open(outfile1, 'a') as out1:
        for line in infile:
            name, ratio = process_line(line)
            out1.write(f"{name}\t{ratio}\n")
                       
if __name__ == '__main__':
    if len(sys.argv) != 3:
        print("Usage: python sam_filter_coverage80.py <input_file> <output_file1>")
        sys.exit(1)


    inputfile = sys.argv[1]
    outfile1 = sys.argv[2]


    process_file(inputfile, outfile1)
```

筛选出大于80覆盖率的reads

```
awk '{if($2>=0.8)print $1}' <coverage.txt> > <coverage_id.txt>
```

```
seqkit grep -f <coverage_id.txt> <hifi_reads.fastq> -o <output.fastq>
```

### Assemble genomes at different sequencing depths

#### Purpose

查找到最优的深度来组装的细胞器基因组。较低的深度（如 30x 到 50x）通常足以生成高质量的基因组组装。在大多数情况下，30x 的深度对于二倍体物种（如人类、果蝇等）就已经足够。适当的测序深度可以帮助解决基因组中的低覆盖区域、复杂区域或重复区域，使得基因组的组装更加完整、准确。但随着测序深度的增加，**冗余数据**的比例也会增加，尤其是在短读测序的情况下。过多的重复信息会导致计算资源的浪费，增加数据处理的复杂度，特别是在组装和校正的阶段。而在长读测序（如 PacBio 或 Nanopore）中，过高的深度可能导致错误的重复区域（例如伪装的重复序列），这种冗余可能会使得组装变得更加困难。更高的测序深度意味着更多的测序数据、存储需求和处理时间。对于大规模基因组组装，成本也会显著上升，尤其是当目标物种非常庞大或复杂时。

#### Software

##### hifiasm

是一个高效的基因组组装工具，专为 PacBio HiFi 数据设计，可以进行高质量的单倍型解析 de novo 组装。它可以在没有父母数据的情况下进行单倍型解析，并且能够处理 HiFi 读数、Hi-C 数据、以及超长 ONT 数据，用于获得高质量的全基因组装和双倍体基因组的组装。

```
hifiasm -o <output_name> -t32 <input_hifireads>
```

* -o NA12878.asm: 设置输出文件的前缀。
* -t 32: 使用 32 个 CPU 核心。
* -l0: 关闭重复去除（对于近交或同源基因组）。
* --dual-scaf: 启用自我 scaffolding 来提高组装的连续性。
* --h1 和 --h2: 提供 Hi-C 数据的配对文件，通常用于单倍型解析。
* --ul file_name: 使用超长的 ONT 读数进行组装。
* -f0: 禁用 Bloom filter，适用于小型基因组。

#### Pipeline

从总的reads中筛选出不同测序深度的reads为后续的组装做准备

`python filter_reads_by_length.py <input_file> <target_length> <output_file>`

```python
import random
import sys

def filter_reads_by_length(input_file, target_length, output_file):
    # 初始化变量
    current_length = 0
    selected_reads = []

    # 读取 FASTQ 文件
    with open(input_file, "r") as infile:
        lines = infile.readlines()

    # 获取所有 reads 的索引
    read_indices = list(range(0, len(lines), 4))
    random.shuffle(read_indices)  # 随机打乱

    # 动态筛选 reads，直到达到目标长度
    for i in read_indices:
        read = lines[i:i+4]  # 获取一个完整的 read
        read_length = len(read[1].strip())  # 第二行是序列

        if current_length + read_length <= target_length:
            selected_reads.extend(read)
            current_length += read_length
        else:
            break

    # 写入输出文件
    with open(output_file, "w") as outfile:
        outfile.writelines(selected_reads)

    print(f"Selected {len(selected_reads)//4} reads with total length {current_length} bp")

if __name__ == "__main__":
    # 检查参数
    if len(sys.argv) != 4:
        print("Usage: python script.py <input_file> <target_length> <output_file>")
        sys.exit(1)

    # 获取命令行参数
    input_file = sys.argv[1]
    target_length = int(sys.argv[2])
    output_file = sys.argv[3]

    # 运行过滤函数
    filter_reads_by_length(input_file, target_length, output_file)
```

基因组的组装

```
hifiasm -o <output name> -t <线程> <reads.fastq>
```

将组装后的gfa文件转化为fasta文件

```
awk '/^S/{print ">"$2;print $3}' <.bp.p_ctg.gfa> > <.fa>
```

### Visual collinearity analysis

同理使用`nucmer`将梯度组装的基因组与参考基因组比对，可视化比对后相似区域的共线性分析

```
nucmer -p <output name> <genome1.fa> <genome2.fa>
```

```
show-coords -r -T <output.delta> > <output.txt>
```

提取出所需可视化的部分

```
awk 'NR > 4 {print $1, $2, $8, $3, $4, $9}' <output.txt> > <filter_output.txt>
```

参考delta文件格式。提取两个基因组分别比对上的区域。因为前4行没有信息，跳过前四行

提取出两个比对基因组的信息

```
bioawk -c fastx '{ print $name, length($seq) }' <genome1> <genome2> > <length.txt>
```

使用R脚本绘图

```R
# 加载必要的包
library(circlize)
library(RColorBrewer) # 好看的颜色！

# 加载基因组长度数据
genome <- read.table("ength.txt", header = FALSE, stringsAsFactors = FALSE)
colnames(genome) <- c("chr", "length")
# 加载共线性数据
synteny <- read.table("genome1_vs_genome2_link.txt", header = FALSE, stringsAsFactors = FALSE)
colnames(synteny) <- c("query_start", "query_end","query_chr",  "target_start", "target_end", "target_chr") # 与我提取128349列有关


# 环
# 初始化染色体环形布局
circos.initialize(factors = genome$chr, xlim = cbind(0, genome$length))

# 绘制基因组的染色体信息
circos.trackPlotRegion(factors = genome$chr, ylim = c(0, 1), 
                       track.height = 0.05,  # 缩小边缘
                       panel.fun = function(x, y) {
                         circos.text(CELL_META$xcenter, 1.8, CELL_META$sector.index, 
                                     cex = 0.5, col = "black", adj = c(0.5, 0))  
                       })
# 绘制共线性关系
colors <- brewer.pal(3, "Set3")[1:length(unique(synteny$target_chr))] # 让一个也可以上色
for(i in 1:nrow(synteny)) {
  color <- colors[which(genome$chr == synteny$query_chr[i]) %% length(colors) + 1]  # 根据染色体选择颜色
  circos.link(synteny$query_chr[i], c(synteny$query_start[i], synteny$query_end[i]), 
              synteny$target_chr[i], c(synteny$target_start[i], synteny$target_end[i]), 
              col = color, lwd = 2)  # 使用选定的颜色
}
```

### Result

![resurt](/img/img-organelle_assemble/3.png)
