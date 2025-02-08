---
title: Python Module -- csv
date: 2025-01-04 21:10
categories: Foundation of programming
tags:
    - "Python"
    - "Python module"
    - "Programe"
excerpt: false
---

{% notel blue 提示 %}

Python内置的官方module不好用，针对CSV文件超处理常用第三方库Pandas

{% endnotel %}

## CSV

**CSV** 是 **Comma-Separated Values** 的缩写，中文常翻译为“逗号分隔值”或“逗号分隔文件”。它是一种用**纯文本**格式存储表格数据的文件类型，广泛用于数据交换和存储。

### 读取

`delimiter = '#', quotechar = '|'`中指定的是数据间分割与数据左右两边的符号。默认的分割是`,`与`""`。

```python
import csv

with oprn('resourse.csv', encoding = 'utf-8') as file
	reader = csv.reader(file, delimiter = '#', quotechar = '|')
  	for row in reader:
      print(row)
```

### 写入

```python
import csv

with oprn('resourse.csv', ‘w’, encoding = 'utf-8') as file2
	writer.writerow(['ID','temperture','information'])
```

