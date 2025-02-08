---
title: Foundation of Python
date: 2024-12-24 19:28
categories: Foundation of programming
tags:
    - "Python"
    - "Programe"
excerpt: false
---

## 语言元素

### 数据类型

- 整型：Python中可以处理任意大小的整数（Python 2.x中有`int`和`long`两种类型的整数，但这种区分对Python来说意义不大，因此在**Python 3.x中整数只有int这一种**了），而且支持二进制（如`0b100`，换算成十进制是4）、八进制（如`0o100`，换算成十进制是64）、十进制（`100`）和十六进制（`0x100`，换算成十进制是256）的表示法。
- 浮点型：浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的，浮点数除了数学写法（如`123.456`）之外还支持科学计数法（如`1.23456e2`）。
- 字符串型：字符串是以单引号或双引号括起来的任意文本，比如`'hello'`和`"hello"`,字符串还有原始字符串表示法、字节字符串表示法、Unicode字符串表示法，而且可以书写成多行的形式（用三个单引号或三个双引号开头，三个单引号或三个双引号结尾）。
- 布尔型：布尔值只有`True`、`False`两种值，要么是`True`，要么是`False`，在Python中，可以直接用`True`、`False`表示布尔值（请注意大小写），也可以通过布尔运算计算出来（例如`3 < 5`会产生布尔值`True`，而`2 == 1`会产生布尔值`False`）。
- 复数型：形如`3+5j`，跟数学上的复数表示一样，唯一不同的是虚部的`i`换成了`j`。实际上，这个类型并不常用，大家了解一下就可以了。

### 运算符

| 运算符                                                       | 描述                           |
| ------------------------------------------------------------ | ------------------------------ |
| `[]` `[:]`                                                   | 下标，切片                     |
| `**`                                                         | 指数                           |
| `~` `+` `-`                                                  | 按位取反, 正负号               |
| `*` `/` `%` `//`                                             | 乘，除，模，整除               |
| `+` `-`                                                      | 加，减                         |
| `>>` `<<`                                                    | 右移，左移                     |
| `&`                                                          | 按位与                         |
| `^` `\|`                                                     | 按位异或，按位或               |
| `<=` `<` `>` `>=`                                            | 小于等于，小于，大于，大于等于 |
| `==` `!=`                                                    | 等于，不等于                   |
| `is`  `is not`                                               | 身份运算符                     |
| `in` `not in`                                                | 成员运算符                     |
| `not` `or` `and`                                             | 逻辑运算符                     |
| `=` `+=` `-=` `*=` `/=` `%=` `//=` `**=` `&=` `|=` `^=` `>>=` `<<=` | （复合）赋值运算符             |

### 特殊

* 如果代码太长写成一行不便于阅读 可以使用`\` 对代码进行折行（换行）

* 在使用`print`函数输出时，也可以对字符串内容进行格式化处理。字符串`%.1f`是一个占位符，稍后会由一个`float`类型的变量值替换掉它。同理，如果字符串中有`%d`，后面可以用一个`int`类型的变量值替换掉它，而`%s`会被字符串的值替换掉。除了这种格式化字符串的方式外，还可以用下面的方式来格式化字符串，其中`{f:.1f}`和`{c:.1f}`可以先看成是`{f}`和`{c}`，表示输出时会用变量`f`和变量`c`的值替换掉这两个占位符，后面的`:.1f`表示这是一个浮点数，小数点后保留1位有效数字。

   ```Python
   print('%.1f华氏度 = %.1f摄氏度' % (f, c))
   print(f'{f:.1f}华氏度 = {c:.1f}摄氏度')
   ```


## 分支结构

```python
score = float(input('请输入成绩: '))
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'E'
print(f'您的成绩是: {score:.2f}，对应的等级是: {grade}')
```

## 循环结构

### for-in

```python
sum = 0
for x in range(2, 101, 2): # 从2起，到101（不包括101）步长2
    sum += x
print(sum)
```

### while

构造不知道具体循环次数的循环结构。`while`循环通过一个能够产生或转换出`bool`值的表达式来控制循环，表达式的值为`True`则继续循环；表达式的值为`False`则结束循环。

```python
import random

answer = random.randint(1, 100)
counter = 0
while True:
    counter += 1
    number = int(input('请输入: '))
    if number < answer:
        print('大一点')
    elif number > answer:
        print('小一点')
    else:
        print('恭喜你猜对了!')
        break # 注意break到位置，如果删除前tap，就不能循环猜。放弃本次循环后续的代码直接让循环进入下一轮
print('你总共猜了%d次' % counter)
if counter > 7:
    print('你的智商余额明显不足')
```

## 函数与模块调用

### 内置函数

| 函数    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| `abs`   | 返回一个数的绝对值，例如：`abs(-1.3)`会返回`1.3`。           |
| `bin`   | 把一个整数转换成以`'0b'`开头的二进制字符串，例如：`bin(123)`会返回`'0b1111011'`。 |
| `chr`   | 将Unicode编码转换成对应的字符，例如：`chr(8364)`会返回`'€'`。 |
| `hex`   | 将一个整数转换成以`'0x'`开头的十六进制字符串，例如：`hex(123)`会返回`'0x7b'`。 |
| `input` | 从输入中读取一行，返回读到的字符串。                         |
| `len`   | 获取字符串、列表等的长度。                                   |
| `max`   | 返回多个参数或一个可迭代对象中的最大值，例如：`max(12, 95, 37)`会返回`95`。 |
| `min`   | 返回多个参数或一个可迭代对象中的最小值，例如：`min(12, 95, 37)`会返回`12`。 |
| `oct`   | 把一个整数转换成以`'0o'`开头的八进制字符串，例如：`oct(123)`会返回`'0o173'`。 |
| `open`  | 打开一个文件并返回文件对象。                                 |
| `ord`   | 将字符转换成对应的Unicode编码，例如：`ord('€')`会返回`8364`。 |
| `pow`   | 求幂运算，例如：`pow(2, 3)`会返回`8`；`pow(2, 0.5)`会返回`1.4142135623730951`。 |
| `print` | 打印输出。                                                   |
| `range` | 构造一个范围序列，例如：`range(100)`会产生`0`到`99`的整数序列。 |
| `round` | 按照指定的精度对数值进行四舍五入，例如：`round(1.23456, 4)`会返回`1.2346`。 |
| `sum`   | 对一个序列中的项从左到右进行求和运算，例如：`sum(range(1, 101))`会返回`5050`。 |
| `type`  | 返回对象的类型，例如：`type(10)`会返回`int`；而` type('hello')`会返回`str`。 |

### 可变参数、位置参数、关键词参数

**可变参数 (args)**：args 允许你传递任意数量的位置参数，函数内部将其作为一个元组处理。

```python
def add(a=0, b=0, c=0):
    """三个数相加"""
    return a + b + c

  
print(add(c=50, a=100, b=200))  # 传递参数时可以不按照设定的顺序进行传递
print(add(1)) # 不指定bc会按默认0
  
def sum_numbers(*args):
    total = 0
    for num in args:
        total += num
    return total

# 调用函数时传递不同数量的参数
print(sum_numbers(1, 2, 3))           # 输出 6 (1 + 2 + 3)
print(sum_numbers(10, 20, 30, 40))    # 输出 100 (10 + 20 + 30 + 40)
print(sum_numbers(5, 10))             # 输出 15 (5 + 10)
print(sum_numbers(100))               # 输出 100
print(sum_numbers())                  # 输出 0 （没有传递参数）
```

调用函数时，如果希望函数的调用者必须以`参数名=参数值`的方式传参，可以用**命名关键字参数**（keyword-only argument）取代位置参数。所谓命名关键字参数，是在函数的参数列表中，写在`*`之后的参数。

```python
def is_triangle(*, a, b, c):
    print(f'a = {a}, b = {b}, c = {c}')
    return a + b > c and b + c > a and a + c > b


# TypeError: is_triangle() takes 0 positional arguments but 3 were given
# print(is_triangle(3, 4, 5))
# 传参时必须使用“参数名=参数值”的方式，位置不重要
print(is_triangle(a=3, b=4, c=5))
print(is_triangle(c=5, b=4, a=3))
```

关键字参数与位置参数

`*args`：用于接收任意数量的**位置参数**，将它们作为**元组处理**。`**kwargs`：用于接收任意数量的**关键字参数**，将它们作为**字典处理**。也因为是字典，所以提取值的时候用`kwargs.values()`获取键值对的值。

```python
def calc(*args, **kwargs):
    result = 0
    for arg in args:
        if type(arg) in (int, float):
            result += arg
    for value in kwargs.values():
        if type(value) in (int, float):
            result += value
    return result


print(calc())                  # 0
print(calc(1, 2, 3))           # 6
print(calc(a=1, b=2, c=3))     # 6
print(calc(1, 2, c=3, d=4))    # 10
```

### 函数嵌套

**函数本身也可以作为函数的参数或返回值**，将上面的`calc`函数不仅仅可以做多个参数求和，还可以做多个参数求乘积甚至更多的二元运算。**调用函数需要在函数名后面跟上圆括号，而把函数作为参数时只需要函数名即可**.如何打圆括号得到的是函数计算得到的值

```python
def calc(*args, init_value, op, **kwargs):
    result = init_value
    for arg in args: # 遍历 args 中的所有值
        if type(arg) in (int, float):
            result = op(result, arg)
    for value in kwargs.values(): # 遍历 kwargs 中的所有值
        if type(value) in (int, float):
            result = op(result, value)
    return result
  
  
def add(x, y):
    return x + y


def mul(x, y):
    return x * y


print(calc(1, 2, 3, init_value=0, op=add, x=4, y=5))      # 15
print(calc(1, 2, x=3, y=4, z=5, init_value=1, op=mul))    # 120
```

### Lambda函数

如果作为参数或者返回值的函数本身非常简单，一行代码就能够完成，那么我们可以使用**Lambda函数**来表示。Python中的Lambda函数是没有的名字函数，所以很多人也把它叫做**匿名函数**，匿名函数只能有一行代码，代码中的表达式产生的运算结果就是这个匿名函数的返回值。

```python
def calc(*args, init_value, op, **kwargs):
    result = init_value
    for arg in args: # 遍历 args 中的所有值
        if type(arg) in (int, float):
            result = op(result, arg)
    for value in kwargs.values(): # 遍历 kwargs 中的所有值
        if type(value) in (int, float):
            result = op(result, value)
    return result
  
print(calc(1, 2, 3, init_value=0, op=lambda x, y: x + y, x=4, y=5)) # 15
print(calc(1, 2, x=3, y=4, z=5, init_value=1, op=lambda x, y: x * y)) # 120
```

Python 标准库中两个非常常用的模块，它们提供了许多用于操作函数、对象和数据的工具。

```python
from operator import mul
from functools import reduce

numbers = [1, 2, 3, 4]
result = reduce(mul, numbers)  # 等同于 1 * 2 * 3 * 4
print(result)  # 输出：24
```

归约(reduce)的意义

```python
from functools import reduce

# 累加列表中的所有元素
result = reduce(lambda x, y: x + y, [1, 2, 3, 4])
print(result)  # 输出：10
```

 1.	初始：x=1（第一个元素），y=2（第二个元素），执行 1 + 2 = 3。

2. 累积：x=3（前一步结果），y=3（第三个元素），执行 3 + 3 = 6。

3. 累积：x=6（前一步结果），y=4（第四个元素），执行 6 + 4 = 10。

4. 返回结果：10。

### 函数的自我调用

计算递归 -- 计算阶乘

```python
def fac(num:int)->int: # -> 是函数注解的一部分，它用于标注函数的返回值类型
    if num == 0: # 收敛条件
        return 1
    return num * fac(num - 1)


if __name__ == '__main__':
   print(fac(10))
```

### 模块导入

在使用`import`导入别的py文件中的函数的时候，不会运行不会执行模块中if条件成立时的代码 因为模块的名字是py文件的名字而不是__main__

`module3.py`

```python
def foo():
    pass


def bar():
    pass


# __name__是Python中一个隐含的变量它代表了模块的名字
# 只有被Python解释器直接执行的模块的名字才是__main__
if __name__ == '__main__':
    print('call foo()')
    foo()
    print('call bar()')
    bar()
```

`test.py`

```python
import module3

# 导入module3时 不会执行模块中if条件成立时的代码 因为模块的名字是module3而不是__main__
```

### 变量作用域

```python
def foo():
    b = 'hello'

    # Python中可以在函数内部再定义函数
    def bar():
        c = True
        print(a)
        print(b)
        print(c)

    bar()
    # print(c)  # NameError: name 'c' is not defined


if __name__ == '__main__':
    a = 100
    # print(b)  # NameError: name 'b' is not defined
    foo()
    
# 100
# hello
# True
```

最终if之后的变量a是一个全局变量（global variable）。函数中的a是局部变量。

* b = 'hello' 是在函数 foo 内定义的局部变量，只能在 foo 内部访问
* 函数内部再定义的函数 bar 是 foo 的局部作用域的一部分，它可以访问 foo 中的变量
* c = True 是在 bar 中定义的局部变量，只能在 bar 内部访问

### 装饰器

装饰器是Python中**用一个函数装饰另外一个函数或类并为其提供额外功能**的语法现象。装饰器本身是一个函数，它的参数是被装饰的函数或类，它的返回值是一个带有装饰功能的函数。	允许我们在不改动函数源码的情况下，动态调整函数的功能

```python
import time

def decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        end_time = time.time()
        print(f'{func.__name__} execution time: {end_time - start_time} seconds.')
        result = func(*args, **kwargs)
        return result
    return wrapper

@decorator
def square(x):
    return x * x

square(10)
```

可以定义定义装饰器的函数 -- 装饰器生成器

```python
import time

def timer(threshold):
    def decorator(func):
        def wrapper(*args, **kwargs):
            start = time.time()
            result = func(*args, **kwargs)
            end = time.time()
            if end - start > threshold:
                print(f'{func.__name__} took over than {threshold} seconds')
            return result
        return wrapper
    return decorator

@timer(0.2)
def sleep_04():
    time.sleep(0.5)

sleep_04()
```

可以使用装饰器自定义库里的函数

## 常用数据结构

### 列表

**列表是由一系元素按特定顺序构成的数据序列**，这样就意味着定义一个列表类型的变量，**可以保存多个数据**，而且**允许有重复的数据**。

在Python中，可以使用`[]`字面量语法来定义列表，列表中的多个元素用逗号进行分隔，代码如下所示。除此以外，还可以通过Python内置的`list`函数将其他序列变成列表。准确的说，`list`并不是一个普通的函数，它是创建列表对象的构造器

```python
items1 = list(range(1, 10))
print(items1)    # [1, 2, 3, 4, 5, 6, 7, 8, 9]
items2 = list('hello')
print(items2)    # ['h', 'e', 'l', 'l', 'o']
```

* 拼接：`+`。注意不是每一项一一对应累加
* 重复：`*`
* 成员运算：`print(100 in items3)`，输出布尔值
*  索引：对于有`N`个元素的列表，正向索引的范围是`0`到`N-1`，负向索引的范围是`-1`到`-N`
* 切片：`[start:stop:step]`。反转序列步长用-1
* 比较运算：`==`两个列表比较相等性比的是对应索引位置上的元素是否相等

#### 列表元素的遍历

如果想逐个取出列表中的元素，可以使用`for`循环

```python
items = ['Python', 'Java', 'Go', 'Kotlin']

for item in items:
    print(item)
```

#### 列表元素的操作

* 尾部添加：`.append`
* 指定位置添加：`.insert`
* 删除指定元素：`.remove`
* 删除指定位置：`.pop`
* 统计一个元素在列表中出现的次数：`.count`
* 排序与反转：`.reverse`、`.sort`

```python
items = ['Python', 'Java', 'Go', 'Kotlin']

# 使用append方法在列表尾部添加元素
items.append('Swift')
print(items)    # ['Python', 'Java', 'Go', 'Kotlin', 'Swift']
# 使用insert方法在列表指定索引位置插入元素
items.insert(2, 'SQL')
print(items)    # ['Python', 'Java', 'SQL', 'Go', 'Kotlin', 'Swift']

# 删除指定的元素
items.remove('Java')
print(items)    # ['Python', 'SQL', 'Go', 'Kotlin', 'Swift']
# 删除指定索引位置的元素
items.pop(0)
items.pop(len(items) - 1)
print(items)    # ['SQL', 'Go', 'Kotlin']

# 清空列表中的元素
items.clear()
print(items)    # []
```

#### 生成示创建列表

```python
# 创建一个由1到9的数字构成的列表
items1 = [x for x in range(1, 10)]
print(items1)    # [1, 2, 3, 4, 5, 6, 7, 8, 9]

# 创建一个由'hello world'中除空格和元音字母外的字符构成的列表
items2 = [x for x in 'hello world' if x not in ' aeiou']
print(items2)    # ['h', 'l', 'l', 'w', 'r', 'l', 'd']

# 创建一个由个两个字符串中字符的笛卡尔积构成的列表
items3 = [x + y for x in 'ABC' for y in '12']
print(items3)    # ['A1', 'A2', 'B1', 'B2', 'C1', 'C2']
```

### 元组

在Python中，元组也是多个元素按照一定的顺序构成的序列。元组和列表的不同之处在于，元组是不可变类型，这就意味着元组类型的变量一旦定义，其中的元素不能再添加或删除，而且元素的值也不能进行修改。定义元组通常使用`()`字面量语法.元组类型支持的运算符跟列表是一样,

```python
# 定义一个三元组
t1 = (30, 10, 55)
# 定义一个四元组
t2 = ('Yuchen', 18, True, '地点')

# 查看变量的类型
print(type(t1), type(t2))    # <class 'tuple'> <class 'tuple'>
# 查看元组中元素的数量
print(len(t1), len(t2))      # 3 4

# 通过索引运算获取元组中的元素
print(t1[0], t1[-3])         # 30 18
print(t2[3], t2[-1])         # 地点 地点

# 循环遍历元组中的元素
for member in t2:
    print(member)

# 成员运算
print(100 in t1)    # False
print(40 in t2)     # True

# 拼接
t3 = t1 + t2        

# 切片
print(t3[::3])      # 30 yuchen 地点

# 比较运算
print(t1 == t3)    # False
print(t1 >= t3)    # False
print(t1 < (30, 11, 55))    # True
```

{% notel red note %}

`()`表示空元组，但是如果元组中只有一个元素，需要加上一个逗号，否则`()`就不是代表元组的字面量语法，而是改变运算优先级的圆括号，所以`('hello', )`和`(100, )`才是一元组，而`('hello')`和`(100)`只是字符串和整数

{% endnotel %}

#### 元组运用

##### 打包解包操作

```python
a = 1, 10, 100, 1000
i, j, *k = a
print(i, j, k)          # 1 10 [100, 1000]
i, *j, k = a
print(i, j, k)          # 1 [10, 100] 1000

# 解包语法对所有的序列都成立
a, b, c = [1, 10, 100]
print(a, b, c)					# 1 10 100
a, *b, c = 'hello'
print(a, b, c)          # h ['e', 'l', 'l'] o
```

##### 交换两个值

可以不用中间变量实现

```python
a, b, c = b, c, a
```

{% notel green Summery %}

**列表和元组都是容器型的数据类型**，即一个变量可以保存多个数据。**列表是可变数据类型**，**元组是不可变数据类型**，所以列表添加元素、删除元素、清空、排序等方法对于元组来说是不成立的。但是列表和元组都可以进行**拼接**、**成员运算**、**索引和切片**这些操作.

{% endnotel %}

### 字符串

在Python程序中，如果我们把单个或多个字符用**单引号或者双引号**包围起来，就可以表示一个字符串。字符串中的字符可以是特殊符号、英文字母、中文字符、日文的平假名或片假名、希腊字母、Emoji字符等。

字符串同样具有着拼接重复、比较、成员计算、索引切片、遍历操作方法，与列表类似。

#### 字符串的方法

在Python中，我们可以通过字符串类型自带的方法对字符串进行操作和处理，对于一个字符串类型的变量，我们可以用`变量名.方法名()`的方式来调用它的方法。

* 首字母大写：`.capitalize`

* 每个单词首字母大写：`.title`

* 所有字母大写：`.upper`

* 所有字母小写：`.lower`

* 查找返回索引位置：`.find`、`.index`

* 查询字符串开头、结尾：`.startswith`、`.endswith`

* 查询字符串是否为纯数字、纯字母、混合构成：`.isdigit`、`.isalpha`、`.isalnum`

* 格式化字符串

  ```python
  s = 'hello, world'
  
  # center方法以宽度20将字符串居中并在两侧填充*
  print(s.center(20, '*'))  # ****hello, world****
  # rjust方法以宽度20将字符串右对齐并在左侧填充空格
  print(s.rjust(20))        #         hello, world
  # ljust方法以宽度20将字符串左对齐并在右侧填充~
  print(s.ljust(20, '~'))   # hello, world~~~~~~~~
  # 在字符串的左侧补零
  print('33'.zfill(5))      # 00033
  print('-33'.zfill(5))     # -0033
  ```

  ```python
  a = 321
  b = 123
  print('%d * %d = %d' % (a, b, a * b))
  print('{0} * {1} = {2}'.format(a, b, a * b))
  print(f'{a} * {b} = {a * b}')
  ```

* 修剪

  ```python
  s = '   jackfrued@126.com  \t\r\n'
  # strip方法获得字符串修剪左右两侧空格之后的字符串
  print(s.strip())    # jackfrued@126.com
  ```

* 替换

  ```python
  s = 'hello, world'
  print(s.replace('o', '@'))     # hell@, w@rld
  print(s.replace('o', '@', 1))  # hell@, world
  ```

* 拆分/合并操作

  ```python
  s = 'I love you'
  words = s.split()
  print(words)            # ['I', 'love', 'you']
  print('#'.join(words))  # I#love#you
  
  s = 'I#love#you#so#much'
  words = s.split('#')
  print(words)            # ['I', 'love', 'you', 'so', 'much']
  words = s.split('#', 3)
  print(words)            # ['I', 'love', 'you', 'so#much']
  ```

### 集合

  1. **无序性**：一个集合中，每个元素的地位都是相同的，元素之间是无序的。
  2. **互异性**：一个集合中，任何两个元素都是不相同的，即元素在集合中只能出现一次。
  3. **确定性**：给定一个集合和一个任意元素，该元素要么属这个集合，要么不属于这个集合，二者必居其一，不允许有模棱两可的情况出现。

在Python中，创建集合可以使用`{}`字面量语法，`{}`中需要至少有一个元素，因为没有元素的`{}`并不是空集合而是一个空字典。也可以使用内置函数`set`来创建一个集合。

```python
# 创建集合的生成式语法(将列表生成式的[]换成{})
set4 = {num for num in range(1, 20) if num % 3 == 0 or num % 5 == 0}
print(set4)         # {3, 5, 6, 9, 10, 12, 15, 18}
```

#### 集合的运算

```python
set1 = {1, 2, 3, 4, 5, 6, 7}
set2 = {2, 4, 6, 8, 10}

# 交集
# 方法一: 使用 & 运算符
print(set1 & set2)                # {2, 4, 6}
# 方法二: 使用intersection方法
print(set1.intersection(set2))    # {2, 4, 6}

# 并集
# 方法一: 使用 | 运算符
print(set1 | set2)         # {1, 2, 3, 4, 5, 6, 7, 8, 10}
# 方法二: 使用union方法
print(set1.union(set2))    # {1, 2, 3, 4, 5, 6, 7, 8, 10}

# 差集
# 方法一: 使用 - 运算符
print(set1 - set2)              # {1, 3, 5, 7}
# 方法二: 使用difference方法
print(set1.difference(set2))    # {1, 3, 5, 7}

# 对称差 -- 属于其中一个集合但不同时属于两个集合的元素
# 方法一: 使用 ^ 运算符
print(set1 ^ set2)                        # {1, 3, 5, 7, 8, 10}
# 方法二: 使用symmetric_difference方法
print(set1.symmetric_difference(set2))    # {1, 3, 5, 7, 8, 10}
# 方法三: 对称差相当于两个集合的并集减去交集
print((set1 | set2) - (set1 & set2))      # {1, 3, 5, 7, 8, 10}
```

集合的交集、并集、差集运算还可以跟赋值运算一起构成复合赋值运算

```python
set1 = {1, 3, 5, 7}
set2 = {2, 4, 6}
# 将set1和set2求并集再赋值给set1
# 也可以通过set1.update(set2)来实现
set1 |= set2
print(set1)    # {1, 2, 3, 4, 5, 6, 7}
set3 = {3, 6, 9}
# 将set1和set3求交集再赋值给set1
# 也可以通过set1.intersection_update(set3)来实现
set1 &= set3
print(set1)    # {3, 6}
```

#### 比较运算

```python
set1 = {1, 3, 5}
set2 = {1, 2, 3, 4, 5}
set3 = set2
# <运算符表示真子集，<=运算符表示子集
print(set1 < set2, set1 <= set2)    # True True
print(set2 < set3, set2 <= set3)    # False True
# 通过issubset方法也能进行子集判断
print(set1.issubset(set2))      # True

# 反过来可以用issuperset或>运算符进行超集判断
print(set2.issuperset(set1))    # True
print(set2 > set1)              # True
```

#### 集合的方法

* 添加元素：`.add`
* 删除指定元素：`.discard`
* 随机删除一个元素并返回：`.pop`
* 清空：`.clear`
* 判断两个集合是否有相同元素：`.isdisjoint`

#### 不可变集合 -- frozenset

Python中还有一种不可变类型的集合，名字叫`frozenset`。`set`跟`frozenset`的区别就如同`list`跟`tuple`的区别，`frozenset`由于是不可变类型，能够计算出哈希码，因此它可以作为`set`中的元素。除了不能添加和删除元素，`frozenset`在其他方面跟`set`基本是一样的。

### 字典

在Python中创建字典可以使用`{}`字面量语法。但是字典的`{}`中的元素是以键值对的形式存在的，每个元素由`:`分隔的两个值构成，`:`前面是键，`:`后面是值.

```python
# 可以通过Python内置函数zip压缩两个序列并创建字典
items1 = dict(zip('ABCDE', '12345'))
print(items1)    # {'A': '1', 'B': '2', 'C': '3', 'D': '4', 'E': '5'}
items2 = dict(zip('ABCDE', range(1, 10)))
print(items2)    # {'A': 1, 'B': 2, 'C': 3, 'D': 4, 'E': 5}

# 用字典生成式语法创建字典
items3 = {x: x ** 3 for x in range(1, 6)}
print(items3)     # {1: 1, 2: 8, 3: 27, 4: 64, 5: 125}
```

**字典中的键必须是不可变类型**，例如整数（`int`）、浮点数（`float`）、字符串（`str`）、元组（`tuple`）等类型的值；显然，列表（`list`）和集合（`set`）是不能作为字典中的键的，当然字典类型本身也不能再作为字典中的键，因为字典也是可变类型，但是字典可以作为字典中的值。

```python
person = {'name': '王大锤', 'age': 55, 'weight': 60, 'office': '科华北路62号'}

# 检查name和tel两个键在不在person字典中
print('name' in person, 'tel' in person)    # True False

# 通过age修将person字典中对应的值修改为25
if 'age' in person:
    person['age'] = 25
    
# 通过索引操作向person字典中存入新的键值对
person['tel'] = '13122334455'
person['signature'] = '你的男朋友是一个盖世垃圾，他会踏着五彩祥云去迎娶你的闺蜜'
print('name' in person, 'tel' in person)    # True True

# 检查person字典中键值对的数量
print(len(person))    # 6

# 对字典的键进行循环并通索引运算获取键对应的值
for key in person:
    print(f'{key}: {person[key]}')
```

#### 字典的方法

* 字典嵌套

  ```py
  # 字典中的值又是一个字典(嵌套的字典)
  students = {
      1001: {'name': '狄仁杰', 'sex': True, 'age': 22, 'place': '山西大同'},
      1002: {'name': '白元芳', 'sex': True, 'age': 23, 'place': '河北保定'},
      1003: {'name': '武则天', 'sex': False, 'age': 20, 'place': '四川广元'}
  }
  ```

* 获取键对应的值

  ```python
  # 使用get方法通过键获取对应的值，如果取不到不会引发KeyError异常而是返回None或设定的默认值
  print(students.get(1002))    # {'name': '白元芳', 'sex': True, 'age': 23, 'place': '河北保定'}
  print(students.get(1005))    # None
  print(students.get(1005, {'name': '无名氏'}))    # {'name': '无名氏'}
  ```

* 获取所有键、值、键值对

  ```python
  # 获取字典中所有的键
  print(students.keys())      # dict_keys([1001, 1002, 1003])
  # 获取字典中所有的值
  print(students.values())    # dict_values([{...}, {...}, {...}])
  # 获取字典中所有的键值对
  print(students.items())     # dict_items([(1001, {...}), (1002, {....}), (1003, {...})])
  # 对字典中所有的键值对进行循环遍历
  for key, value in students.items():
      print(key, '--->', value)
  ```

* 删除元素

  ```python
  person = {'name': '王大锤', 'age': 25, 'sex': True}
  del person['age']
  print(person)    # {'name': '王大锤', 'sex': True}
  ```

Python程序中的字典跟现实生活中字典非常像，允许我们**以键值对的形式保存数据**，再**通过键索引对应的值**。这是一种非常**有利于数据检索**的数据类型，底层原理我们在后续的课程中为大家讲解。再次提醒，**字典中的键必须是不可变类型**，字典中的值可以是任意类型。

### 不同数据结构的打包解包

```python
dict1 = {'a':1, 'b':2}
dict2 = {'c':3, 'd':4}
list1 = [1,2,3,4,5]
tuple1 = (1,2,3,4,5)

# 一个星操作的是序列，两个操作的是字典
merged1 = {**dict1, **dict2}
merged2 = {*list1, *tuple1}
```

## 面向对象的编程

**面向对象编程**：把一组数据和处理数据的方法组成**对象**，把行为相同的对象归纳为**类**，通过**封装**隐藏对象的内部细节，通过**继承**实现类的特化和泛化，通过**多态**实现基于对象类型的动态分派。



通过`__init__`方法在创建对象时为对象绑定了属性并赋予了初始值。在Python中，以两个下划线`__`（读作“dunder”）开头和结尾的方法通常都是有特殊用途和意义的方法，我们一般称之为**魔术方法**或**魔法方法**.

```python
class Student:
    """学生"""

    def __init__(self, name, age):
        """初始化方法"""
        self.name = name
        self.age = age

    def study(self, course_name):
        """学习"""
        print(f'{self.name}正在学习{course_name}.')

    def play(self):
        """玩耍"""
        print(f'{self.name}正在玩游戏.')
    
    def __repr__(self): 
      # print(stu1).印对象的时候不希望看到对象的地址而是看到我们自定义的信息
        return f'{self.name}: {self.age}'


stu1 = Student('骆昊', 40)
stu1.study('Python程序设计')    # 骆昊正在学习Python程序设计.
stu2.play()                    # 王大锤正在玩游戏.
print(stu1)        # 骆昊: 40
students = [stu1, Student('李元芳', 36), Student('王大锤', 25)]
print(students)    # [骆昊: 40, 李元芳: 36, 王大锤: 25]
```

### 静态方法与类方法

类里面的函数，称为方法，是发给对象的“消息”。但是有些“消息”并不是发给对象的，需要发给类，称为静态方法

```python
class Triangle(object):
    """三角形类"""

    def __init__(self, a, b, c):
        """初始化方法"""
        if not Triangle.is_valid(a, b, c):
            raise ValueError('无效边长')
        self.a = a
        self.b = b
        self.c = c

    @staticmethod
    def is_valid(a, b, c):
        """判断三条边长能否构成三角形(静态方法)   """
        return a + b > c and b + c > a and a + c > b

    # @classmethod
    # def is_valid(cls, a, b, c):
    #     """判断三条边长能否构成三角形(类方法)"""
    #     return a + b > c and b + c > a and a + c > b

    def perimeter(self):
        """计算周长"""
        return self.a + self.b + self.c

    def area(self):
        """计算面积"""
        p = self.perimeter() / 2 # 调用已定义类中的周长
        return (p * (p - self.a) * (p - self.b) * (p - self.c)) ** 0.5
    
    
    
if __name__ == '__main__':
    try:
        t = Triangle(1,2,3)
        print(t.area())
        print(t.perimeter())
    except ValueError as err:
        print(err)
```

### 继承与多态

* 继承的语法是在定义类的时候，在类名后的圆括号中指定当前类的父类
* 子类继承父类的方法后，还可以对方法进行重写（重新实现该方法），不同的子类可以对父类的同一个方法给出不同的实现版本，这样的方法在程序运行时就会表现出多态行为（调用相同的方法，做了不同的事情）。

```python
class Person:
    """人类"""

    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def eat(self):
        print(f'{self.name}正在吃饭.')
    
    def sleep(self):
        print(f'{self.name}正在睡觉.')


class Student(Person):
    """学生类"""
    
    def __init__(self, name, age):
        # super(Student, self).__init__(name, age)
        super().__init__(name, age)
    
    def study(self, course_name):
        print(f'{self.name}正在学习{course_name}.')


class Teacher(Person):
    """老师类"""

    def __init__(self, name, age, title):
        # super(Teacher, self).__init__(name, age)
        super().__init__(name, age)
        self.title = title
    
    def teach(self, course_name):
        print(f'{self.name}{self.title}正在讲授{course_name}.')



stu1 = Student('白元芳', 21)
stu2 = Student('狄仁杰', 22)
teacher = Teacher('武则天', 35, '副教授')
stu1.eat()
stu2.sleep()
teacher.teach('Python程序设计')
stu1.study('Python程序设计')
```

