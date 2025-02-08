---
title: Regulation expression
date: 2025-01-08 14:36
categories: Foundation of programming
tags:
    - "Python"
    - "Programe"
    - "Python module"
excerpt: false
---

## 概述

正则表达式本质是一个匹配字符串的模式，可以满足复杂的匹配规则。

例如检查输入用户名满足数字字母下划线，长度6-20基本写法

字符集`[a-zA-Z0-9]{6,20}`等价于使用元字符`\\w{6,20}`。注意第一个斜杠是转义字符。

| 符号    | 描述                               | 示例      | 匹配结果                  |
| ------- | ---------------------------------- | --------- | ------------------------- |
| `.`     | 匹配任意单个字符（换行符除外）     | `a.b`     | 匹配 "a_b"，如 "acb"      |
| `^`     | 匹配字符串的开头                   | `^abc`    | 匹配以 "abc" 开头的字符串 |
| `$`     | 匹配字符串的结尾                   | `xyz$`    | 匹配以 "xyz" 结尾的字符串 |
| `*`     | 匹配前一个字符 0 次或多次          | `ab*`     | 匹配 "a"、"ab"、"abb" 等  |
| `+`     | 匹配前一个字符 1 次或多次          | `ab+`     | 匹配 "ab"、"abb" 等       |
| `?`     | 匹配前一个字符 0 次或 1 次         | `colou?r` | 匹配 "color" 或 "colour"  |
| `{n}`   | 匹配前一个字符恰好 n 次            | `a{3}`    | 匹配 "aaa"                |
| `{n,}`  | 匹配前一个字符至少 n 次            | `a{2,}`   | 匹配 "aa"、"aaa" 等       |
| `{n,m}` | 匹配前一个字符至少 n 次且至多 m 次 | `a{2,4}`  | 匹配 "aa"、"aaa"、"aaaa"  |
| `|`     | 或，匹配符号两侧的任意一个         | `cat|dog` | 匹配 "cat" 或 "dog"       |
| `()`    | 分组，用于逻辑组合或捕获           | `(ab)+`   | 匹配 "ab"、"abab" 等      |
| `[]`    | 匹配方括号内的任意字符             | `[abc]`   | 匹配 "a"、"b" 或 "c"      |
| `-`     | 在方括号中表示范围                 | `[a-z]`   | 匹配任意小写字母          |
| `\`     | 转义字符，用于匹配特殊字符或元字符 | `\.`      | 匹配 "."                  |

元字符

`+`意思是出现一次或多次

| 符号 | 描述                                   | 示例       | 匹配结果                    |
| ---- | -------------------------------------- | ---------- | --------------------------- |
| `\d` | 匹配任意数字（0-9）                    | `\d{3}`    | 匹配 3 位数字，如 "123"     |
| `\D` | 匹配任意非数字字符                     | `\D+`      | 匹配非数字，如 "abc"        |
| `\w` | 匹配任意单词字符（字母、数字、下划线） | `\w+`      | 匹配 "word123" 或 "abc_123" |
| `\W` | 匹配任意非单词字符                     | `\W+`      | 匹配 "!@#" 等符号           |
| `\s` | 匹配任意空白字符（空格、制表符等）     | `\s+`      | 匹配空格或 Tab              |
| `\S` | 匹配任意非空白字符                     | `\S+`      | 匹配 "abc123"               |
| `\b` | 匹配单词边界                           | `\bword\b` | 匹配完整的 "word"           |
| `\B` | 匹配非单词边界                         | `\Bword`   | 匹配 "sword" 中的 "word"    |

### 用户名合法性检查

python中使用正则表达式两种方式：

* 不创建正则表达式对象，直接调用正则表达式进行匹配操作
* 创建正则表达式对象（pattern），通过调用对象的方法实现匹配操作（如果一个正则表达式要使用多次）

```python
import re

username = input("Enter your username: ")
# 完全匹配的两种方法，注意转义字符
matcher = re.fullmatch('\\w{6,20}', username)
# matcher = re.match('^\\w{6,20}$', username)
if matcher is None:
    print("Invalid username")
    
# 匹配QQ号。第一位不能为0，长度最短5位，最长13位的数字.
qq = input("Enter your QQ: ")
matcher = re.fullmatch('[1,9]\\d{4,12}', username)
```

```python
import re

username = input("Enter your username: ")
username_pattern = re.compile('\\w{6,20}')\

match = username_pattern.match(username)
if match is None:
    print("Invalid username")
else:
    print(match.group()) # 展示出匹配上的对象
```

### 从一段信息中提取匹配信息

复杂信息中提取电话号码

```python
import re

content = "my name is abc, I live in the XXXXX, and my phone number is 13811223344, thank you."

matcher = re.search('1[3-9]\\d{9}', content)
if not matcher:
    print("No find phone number")
else:
    print(matcher.group())
```

取出信息中的所有数字

```python
import re

content = """my name is abc, I live in the XXXXX,
 and my phone number is 13811223344, my qq number is 35267,
 thank you."""

pattern = re.compile(r'\d+')
matcher = pattern.search(content)
while matcher:
    print(matcher.group())
    matcher =pattern.search(content, matcher.end())
    
# 使用findall方法，把所有匹配的放入一个列表中
results = pattern.findall(content)
for result in results:
  print(result)
```

### 从网页上获取新闻标题和链接

```python
import requests
import re

# 匹配href="http开头的列，并且仅可能的短短匹配（？符号）
pattern = re.compile(r'href="http.+?"')
rep = requests.get('https://news.cctv.com/news/world/')
content = rep.text
match  = pattern.search(content)
while match:
    print(match.group()[6:-1]) # 切片得到url
    match = pattern.search(content, match.end())

pattern1 = re.compile(r'title=".+?"')
title_list = pattern1.findall(content)
for title in title_list:
    print(title[7:-1])

```

该方法的不足，不能一一对应。选择从html中提取A标签，之后使用捕获组统计得到的标签和url。

```python
import requests
import re

pattern = re.compile(r'<a/s.*?href="(.+?)".*?title="(.+?)".*?>')
resp = requests.get("https://news.cctv.com/news/world/")
results = pattern.findall(resp.text)
for herf, title in results: # 捕获组得到的是二元组
  print(title)
  print(herf)
```

### 不良内容过滤

```python
import re

contest = ' XXX 是傻逼, Fuck you'
# flag 忽略大小写
modified_contest = re.sub(r'[傻沙煞][逼雕璧]|fuck|shit','*',contest,flags=re.IGNORECASE)
print(modified_contest)
```

### 拆分

```python
import re

poem = '窗前明月光，疑是地上霜。举头望明月，低头思故乡。'
sentences_list = re.split(r'[，。]', poem)
# sentences_list = re.split(r'，｜。', poem)

# 拆完了之后，会多出一个空在最后
sentences_list = [sentence for sentence in sentences_list if sentence]
for sentence in sentences_list:
    print(sentence)
```

