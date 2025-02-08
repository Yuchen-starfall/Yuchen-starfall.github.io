---
title: Python Module -- Pandas
date: 2025-01-20 17:45
categories: Foundation of programming
tags:
    - "Python"
    - "Python module"
    - "Programe"
excerpt: false
---

pandas 是 Python 中用于数据处理和分析的一个强大库，特别适合处理结构化数据。它提供了高效、灵活且易于使用的数据结构和数据分析工具。

* Series：一维数组，类似于列表或一列数据，可以有索引（类似字典的键值对）。
* DataFrame：二维表格型数据结构，类似于电子表格或 SQL 表，拥有行索引和列索引。

### Series

本质理解为是一个有序的字典结构。

#### 使用数组创建

Series包括`.value`和`.index`。Index可以自定义索引.

可以通过对象.索引指定，或者使用中括号制定数字索引（类似于字典操作），例如：`s1.A`，`s1[0]`

```python
import numpy as np
import pandas as pd

list1 = [11,22,33,44]
n = np.array(list1)

s1 = pd.Series(list1)
s2 = pd.Series(n)

s1.index = ['A','B','C','D']
```

#### 使用字典创建

索引是字典的key，值是字典的value

```
d = {
    'a':11,
    'b':22,
    'c':33,
}
n1 = pd.Series(d)
```

#### 索引

可是使用bool值

1. 显式索引：使用中括号方式进行索引`n1[['a','b']]`，`n1.loc[['a','b']]`
2. 隐式索引：0代表第一个数。`n1[[0,2]]`，`n1.iloc[[0,2]]`

#### 切片

1. 使用数字下标。`n1[[1:2]]`，`n1.iloc[[1:2]]`
2. 使用索引名`n1[['b':'c']]`，`n1.loc[['b':'c']]`

#### 基本属性与常用方法

* `.shape`：形状。一维数组，使用元组表示
* `.size`：元素个数
* `.index`
* `.value`
* `.name`
* `.head`:查看数据结构

检测缺失数据

输出为False、True类型

```
s = pd.Series(['张三','李四','王五',np.nan])

s.isnull()
pd.isnull(s)
s.notnull()
pd.notnull(s)
```

通过布尔（bool）值索引过滤数据 -- 删除空值

`~`意思是取反

```
cond1 = s.isnull()
cond2 = s.notnull()
s[~cond1]
s[cond2]
```

#### 运算

两个一位矩阵矩阵是根据**索引相同**的进行计算

series**没有广播机制**：可以使用`s2.add(s1,fill_value=0)`进行计算，用0填充，使得位数相同。

### DataFrame

多列数组组成。将一维数组拓展到多维

```python
import pandas as pd

d = {
    'name':['python','panda'],
    'age':[34,56]
}

df = pd.DataFrame(d)
print(df)
```

#### 基本属性与常用方法

* `.shape`：展示矩阵结构
* `.head`:查看数据结构.value``
* `.tail(3)`:显示后面三条
* `.head(2)`:显示前面两条

行列索引可以在创建时更改`pd.DataFrame(d,index=list('AB'))`

* `df.index = list('AB')`:更改行索引
* `df.columns = ['name2','age2']`:更改列索引

#### 索引

以二维为例

* 列索引`df[['age','name']]`
* 行索引`df.iloc[0]`或`df.loc['小A']`
* 取一个元素，先取列再取行。`df['A']['小A']`。组合使用显式隐式

#### 切片

先对行切片再切列。

* 行切片：`df[1:3]`。**左闭右开区间**
* 列切片：`df.iloc[:,1:3]`

#### 运算

对应索引数的和。同样无广播机制`df1.add(df2,fill_value = 0)`

### 层次化索引

#### 构造

以行层次化索引为例。列索引一样

* 数组方式

```python
import pandas as pd
import numpy as np

data = np.random.randint(0,100,size=(6,6))

index = pd.MultiIndex.from_arrays([
    ['1班','1班','1班','2班','2班','2班'],
    ['A','B','C','D','E','F']
])

columns =[
    ['期中','期中','期中','期末','期末','期末'],
    ['语','数','英','语','数','英']
]

df = pd.DataFrame(data = data,index = index,columns = columns)
print(df)
```

结果

```
      期中          期末        
       语   数   英   语   数   英
1班 A  57  38  85  78  14  78
   B  80  27  71   5  92  41
   C  28  86  13  43  82  71
2班 D  15  37  16  10  32   8
   E  32  53  73  63  86  92
   F  64  51  17  32  54  35
```

* 元组方式

```python
import pandas as pd
import numpy as np

data = np.random.randint(0,100,size=(6,6))

index = pd.MultiIndex.from_tuples(
    (
        ('一班','A'),('一班','B'),('一班','C'),
        ('二班','D'),('二班','E'),('二班','F'),
    )
)

columns =[
    ['期中','期中','期中','期末','期末','期末'],
    ['语','数','英','语','数','英']
]

df = pd.DataFrame(data = data,index = index,columns = columns)
print(df)

```

结果

```
      期中          期末        
       语   数   英   语   数   英
一班 A  75  15   7  83  91  28
   B  51  45  20  63  72  34
   C  59  34  60   6  99  57
二班 D   5  48  35  30  60   5
   E  83  49  51  76  77  33
   F  83  57  55  37  62  70
```

* 笛卡尔积

```python
import pandas as pd
import numpy as np

data = np.random.randint(0,100,size=(6,6))

index = pd.MultiIndex.from_product([
    ['1班','2班'],
    ['A','B','C']
])

columns =[
    ['期中','期中','期中','期末','期末','期末'],
    ['语','数','英','语','数','英']
]

df = pd.DataFrame(data = data,index = index,columns = columns)
print(df)

```

结果

```
      期中          期末        
       语   数   英   语   数   英
1班 A  43  64  28  80  66   7
   B  60  81  53  58  95  72
   C  83  55  65  12  63  97
2班 A  24  67   7   0  23  50
   B  41  40  68  76  43  49
   C  37  77  50  59  54  75
```

