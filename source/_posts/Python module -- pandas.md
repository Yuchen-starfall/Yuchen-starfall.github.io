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

#### 索引、切片

`df['期中']['数']['1班']['A']`使用显式索引提出第一行第二列数据64

`df.iloc[0,1]`，`df.loc[('1班','A'),('期中','数')]`使用隐式索引提出第一行第二列数据64

`df.iloc[:]`

#### 索引堆叠

* 行索引转化为列索引`df.stack()`里面有一个参数level=-1/0/1/...，例如0代表吧最外面一层变成行索引
* 列索引转化为行索引`df.unstack()`，同理，存在level参数

### 数据操作

#### 聚合

* 同一行多列的和`df.sum(axis=1)`
* 同一列多行的和`df.sum(axis=0)`，计算行中的第一层`df.sum(axis=0,level=0)`

同理计算平均值`mean`最大值`sum`

#### 数据合并

* `pd.concat()`

```python
import numpy as np
import pandas as pd

def make_df(indexs,columns):
    data = [[str(j) + str(i) for j in columns] for i in indexs]
    df = pd.DataFrame(data = data,index = indexs,columns=columns)
    return df

df1 = make_df([1,2],list('AB'))
df2 = make_df([3,4],list('AB'))

concat1 = pd.concat([df1,df2])
concat2 = pd.concat([df1,df2],axis=1)
concat3 = pd.concat([df1,df2],ignore_index=True)
concat4 = pd.concat([df1,df2],keys = ['x','y'])
print(df1,df2,concat1,concat2,concat3,concat4,sep='\n\n')
```

```
    A   B
1  A1  B1
2  A2  B2

    A   B
3  A3  B3
4  A4  B4

    A   B
1  A1  B1
2  A2  B2
3  A3  B3
4  A4  B4

     A    B    A    B
1   A1   B1  NaN  NaN
2   A2   B2  NaN  NaN
3  NaN  NaN   A3   B3
4  NaN  NaN   A4   B4

    A   B
0  A1  B1
1  A2  B2
2  A3  B3
3  A4  B4

      A   B
x 1  A1  B1
  2  A2  B2
y 3  A3  B3
  4  A4  B4

```

内匹配与外匹配，参数`join=inner`即取交集，显示共同部分

* `pd.append()`。例子`df1.append(df2)`，结果类似于`concat2 = pd.concat([df1,df2],axis=1)`

* `pd.merge()`，**key用于指定用于连接的列，如果没有相同的列名，使用left_on和right_on分别指定两个表中不同列作为连接字段**。

  * 一对一合并

  ```python
  import pandas as pd
  
  df1 = pd.DataFrame({
      'name':['张三','李四','王五'],
      'id':[1,2,3],
      'age':[22,33,44]
  })
  df2 = pd.DataFrame({
      'id':[2,3,4],
      'sex':['男','女','男'],
      'job':['Saler','CEO','Programer']
  })
  merge = pd.merge(df1,df2,how='left',on='id')
  print(merge)
  ```

  ```
    name  id  age  sex    job
  0   张三   1   22  NaN    NaN
  1   李四   2   33    男  Saler
  2   王五   3   44    女    CEO
  ```

  * 多对一合并

  ```python
  import pandas as pd
  
  df1 = pd.DataFrame({
      'name':['张三','李四','王五'],
      'id':[1,2,2],
      'age':[22,33,44]
  })
  df2 = pd.DataFrame({
      'id':[2,3,4],
      'sex':['男','女','男'],
      'job':['Saler','CEO','Programer']
  })
  merge = pd.merge(df1,df2,how='left',on='id')
  print(merge)
  ```

  ```
    name  id  age  sex    job
  0   张三   1   22  NaN    NaN
  1   李四   2   33    男  Saler
  2   王五   2   44    男  Saler
  ```

  * 多对多合并

  ```python
  import pandas as pd
  
  df1 = pd.DataFrame({
      'name':['张三','李四','王五'],
      'id':[1,2,2],
      'age':[22,33,44]
  })
  df2 = pd.DataFrame({
      'id':[2,2,4],
      'sex':['男','女','男'],
      'job':['Saler','CEO','Programer']
  })
  merge = pd.merge(df1,df2,how='left',on='id')
  print(merge)
  ```

  ```
    name  id  age  sex    job
  0   张三   1   22  NaN    NaN
  1   李四   2   33    男  Saler
  2   李四   2   33    女    CEO
  3   王五   2   44    男  Saler
  4   王五   2   44    女    CEO
  ```

  `how='left'`代表使用左连接，意义是现实左边的所有数据和右边的公共数据

#### 缺失值数据

* `.isnull`、`.notnull`展示矩阵的每个位置的布尔值
* `all()`必须全为True才是True。`any()`只要有一个True就得到True。
* `df.isnull().any()`常用与找到有空的**列** 。`df.isnull().any(axis=1)`为空的**行**
* `df.notnull().all()`常用与找到不为空的**列**。 

* 对行\列进行过滤，所有没有缺失值的行\列

```python
# 扩展之后可以不针对空值，可以加筛选条件
# 对行进行过滤
cond = df.notnull().all(axis=1)
df[cond]


# 对列进行过滤
cond = df.notnull().all()
df.loc[:,cond]
```

```
# 仅能处理空值
df.dropna() # 删除有空的行
df.dropna(axis=1) # 删除有空的列
df.dropna(how='all') # 仅这一列全是空才删除
```

* 填充空值。`df.fillna(value=0)`，使用`inplace=True`可以改变原数据

#### 重复值

`.duplicated(keep='first')`重复行,保留第一行，和第一行重复显示TRUE。如果想判断一行的某几列重复：`.duplicated(subset=['列名'])`

`.drop_duplicated()`删除。

#### 替换

* `df['列名'].map(lambda x:x*10)` 。map函数仅仅可以可以处理series

* 加一列判断是否及格`df['是否及格']=df['判断列名'].map(lambda n:'及格' if n>60 else '不及格')`

* 修改行索引名`df.rename[('A':'B')]`,修改列索引名`df.rename[('A':'B'),axis=1]`

* 重设置行索引`df.set_index[keys = ['A']]`，重置索引`df.reset_index()`、
* `df.apply(lammbda x:x.mean(),axis=0)`。求每一列数据等平均值
