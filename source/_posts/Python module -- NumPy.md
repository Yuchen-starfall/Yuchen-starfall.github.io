---
title: Python Module -- NumPy
date: 2025-01-14 23:36
categories: Foundation of programming
tags:
    - "Python"
    - "Python module"
    - "Programe"
excerpt: false
---

NumPy (Numerical Python) 是一个开源的数值计算库，用于储存和处理**大型矩阵**。虽然Python中可以嵌套列表表示矩阵，但是因NumPy底层是C编写，运行效率很高，并且针对数组运算有很多大量的数学函数库。

使用Anaconda中的Jupyter Notebook中的**IPython解释器**编写代码

### Jupyter Notebook

* 编辑模式：允许在单元格中输入文本与代码，此时单元格是绿色的
* 命令模式：输入运行程序命令，此时单元格是蓝色

**Keyboard Shoutcuts** -- 忘记了右上角help可以列出

* Toggle between command mode (blue) and edit mode (green) with `Esc` and `Enter`, respectively.
* While in command mode:
  - Scroll up and down your cells with your `Up` and `Down` keys.
  - Press `A` or `B` to insert a new cell above or below the active cell.
  - `M` will transform the active cell to a Markdown cell.
  - `Y` will set the active cell to a code cell.
  - `D + D` (`D` twice) will delete the active cell.
  - `Z` will undo cell deletion.
  - Hold `Shift` and press `Up` or `Down` to select multiple cells at once. With multiple cells selected, `Shift + M` will merge your selection. You can also click and `Shift + Click` in the margin to the left of your cells to select a range of them.
* While in edit mode:
  - `Ctrl + Enter` to run the current cell.
  - `Shift + Enter` to run the current cell and move to the next cell (or create a new one if there isn’t a next cell)
  - `Alt + Enter` to run the current cell and insert a new cell below.
  - `Ctrl + Shift + -` will split the active cell at the cursor.
  - `Ctrl + Click` to create multiple cursors within a cell.

### Numpy

#### Creating a matrix

* `np.array`
* `np.ones(shape,dtype=None,order='C')`（构建一个所有元素都为1的多维数组）
  * Shape:性状
  * dtype=None:元素类型（float,np.int(16)...）
  * order={'C','F'}
* `np.zeros(shape,dtype=float,order='C')`
* `np.full(shape,fill_value,dtype=float,order='C')`
* `np.eye(N,M=None,k=0,dtype=float)`（单位矩阵：行列相等矩阵，构建对角线为1其他位置为0的二位数组）
  * N:行
  * M:列
  * k=0:向右偏移
* `np.linspace(star,stop,num50,endpoint=Ture,retstep=False,dtype=None)`(创建等差数列)
  * star:开始值
  * Stop:结束值
  * num=50:等差数列中默认50个数
  * Endpoint=True:是否包含结束值
  * retstep=False:返回步长
* `np.arange([start,]stop,[step,]dtype=None)`
* `np.random.randint(low,high=None,size=None,dtype='I')`(随机整数多维数组)
  * 生成‘前闭后开’的随机整数
  * 二维：size=(3,4)三行四列
* `np.random.randn(d0,d1,...,dn)`(服从标准正态分布的多维数组)
  * 0为均数，1为标准差的正态分布
* `np.random.normal(loc=0.0,scale=1.0,size=None)`(服从正态分布的多维数组)
  * loc对应正态分布中心
  * scale标准差

```python
import numpy as np
import pandas as pd

c=[[1,2,3],[4,5,6],[7,8,9]]
d=np.array(c)

n=np.ones(shape=(3,4)) # 三行四列全为1的数组
```

#### Ndarray属性

* `.ndim`:查看维度
* `.shape`:形状
* `.size`:总长度
* `.dtype`:元素类型

#### Ndarray索引

* 一维数组与列表一致，`[0]` (第一个元素)、`[-1]`(最后一个元素)
* 二维数组，`[3,4]`(第4行5列的元素)，多维同理

#### Ndarray切片

* 一维数组，`[2:6]`取第3个到第6个。`[::-1]`翻转
* 二维数组
  * 列
    * 单独。`[:,0]` 取所有行第0列。`[1:4,0]`取第2、3、4行的第0列 
    * 连续多行。`[:,2:5]`取所有行第3-5列
    * 不连续多行。`[:[1,2,4]]`  
  * 行
    * 单独。`[0]` 
    * 连续多行。`[1:4]`
    * 不连续多行。`[[1,2,4]]`  

#### Ndarray数组变形

* `.reshape(a,newshape,order='C')` 
  * Newshape:	
    * (20)一维数组
    * (4,5)四行五列
    * (4,-1)四行，根据数量自动匹配列

#### Ndarray数组级联合并

* `.concatenate()` 
  * 参数是需要合并的两个数组，默认，上下合并
  * 参数`axis=0`及按照第一个维度合并（二维数组即按照行，上下合并）  
  * 参数`axis=1`及按照第二个维度合并（二维数组即按照列，左右合并）  

#### Ndarray数组的拆分

* `.vsplit()` 
  * 两个参数，一个是需要拆分的数组，另一个是需要平均拆为几部份（上下垂直拆分）
  * `.vsplit(n,(1,2,4))`意思是从第1，2，4的位置去拆分 
* `.hsplit()` 
  * 两个参数，一个是需要拆分的数组，另一个是需要平均拆为几部份（左右拆分）
* `.split()` 
  * 参数是需要合并的两个数组，默认，上下拆分
  * 参数`axis=0`及按照第一个维度拆分（二维数组即按照行，上下拆）  
  * 参数`axis=1`及按照第二个维度拆分（二维数组即按照列，左右拆）  

#### Ndarray数组的拷贝

如果使用=赋值进行拷贝，因为两个数组使用同一个内存空间，修改一个另一个会改变。使用`.copy()` 

#### 聚合操作

* `np.sum()`、 `np.mean()`、 `np.medium()`、 `np.percentile()`、`np.std()`（标准差）、`np.var()`（方差）
  * 参数`axis=0`进行列求和
*  `np.min()`、 `np.max()`
* 求第一个最大值**下标**
  * `np.argmax()`
  * `np.angwhere(n==argmax(n))`--所有最大值的下标

#### 矩阵操作

* 乘法
  *  `n1*n2`，两个对应数字相乘
  *  `np.dot(n1,n2)`矩阵点乘，第一个的行与第二个的列相乘
* 矩阵的逆
  *  `np.linalg.inv()`
* 矩阵的行列式
  *  `np.linalg.det()`
* 矩阵的秩
  * `np.linalg.matrix_rank()`

#### 广播机制

两个矩阵维度等不一样，numpy会尽量去计算，通过补缺失的维度、补缺失元素（根据已有元素）

#### 排序

* `np.sort()`不改变原数组，需要用另一个接收排序后的数组
* `ndarray.sort()`改变原数组

#### 文件操作

储存

* `.save(文件名，数组数据)`，储存为npy文件
* `.savez(文件名，数组数据)`，多个数组储存在一个npy文件
* `np.savetxt('名字',n,delimiter=',')`

读取

* `np.load()`
* `np.loadtxt()`

#### 其他常见机制

* `.abs`：绝对值
* `.sqrt`：平方根
* `.square`：平方
* `.exp`：指数，以e为底
* `.round`：四舍五入
* `.cell`：向上去整
* `.floor`：向下去整
* `.cumsum`：累加求和