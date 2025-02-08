---
title: Markdown command
date: 2024-12-14 18:33
categories: Foundation of programming
tags:
    - "Markdown"
    - "Programe"
excerpt: false
---

Markdown是一种轻量级标记语言，专注于简洁易用的语法，用于快速编写格式化的文本（通过特定的样式或排版使文本具有更好的结构和可读性）。它最初由John Gruber在2004年设计，主要用于将纯文本转换为HTML格式。一下以Typora为例，简单的介绍在Mac版本中该种语言的快捷键与语法。

 ## 多级标题

有6级标题

```markdown
# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题
```

Typora 快捷键

⌘+ ⌘- ⌘1～⌘6

##  加粗

```markdown
**word**
```

Typora 快捷键

⌘B

## 倾斜

```markdown
*word*
```

Typora 快捷键

⌘I

## 下划线

```markdown
<u>word</u>
```

Typora 快捷键

⌘U

## 高亮

```markdown
==word==
```

Typora 快捷键

⌘H

## 上下标

```markdown
cm^3^

H~2~O
```

## 无序列表

```markdown
- list1
	- list2
		- list3
```

## 有序列表

```markdown
1. list1
2. list2
3. list3
```

## 勾选任务列表

```markdown
- [x] 早饭
- [ ] 晚饭
- [ ] 午饭
```

Typora 快捷键

⌘⌥X

## 行内代码

```markdown
`code`
```

Typora 快捷键

⌃`

## 代码块

```markdown
```code
```

Typora 快捷键

⌘⌥C

## 行内公式

公式使用的是latex代码

```markdown
$\sin x = 2\sin x \cos x$
```

Typora 快捷键

⌃M

## 公式块

公式使用的是latex代码

可以添加公式序号

```markdown
$$
E_{\rm k} = \frac 1 2 mv^2
\tag{1.1}
$$
```

Typora 快捷键

⌘⌥B

## 列表

```markdown
|           | MON  | TUR  | WED  | THU  | FBI  | SAT  | SUN  |
| :-------: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| Breakfast |      |      |      |      |      |      |      |
|   Lunch   |      |      |      |      |      |      |      |
|  Dinner   |      |      |      |      |      |      |      |
```

Typora 快捷键

⌘⌥T

## 引用

```markdown
> 我没说过这句话。——鲁迅
```

Typora 快捷键

⌘⌥Q

## 链接

```markdown
[bilibili](www.bilibili.com)
[text](URL)
```

Typora 快捷键

⌘⌥L

## 跳转链接(超链接)

```markdown
[text](#name)
不仅可以链接文章中文字，也可以链接图片
[![沙漠中的岩石图片](/assets/img/shiprock.jpg "Shiprock")](https://markdown.com.cn)
```

Typora 快捷键

⌘K

## 插入图片

```markdown
![图片alt](图片链接 "图片title")
```

## 尾注

```markdown
text[^tag]
[^tag]:text
```

Typora 快捷键

⌘⌥R

## 分隔行

```markdown
---
```

Typora 快捷键

⌘⌥-

## 添加目录

```markdown
[TOC]
```

