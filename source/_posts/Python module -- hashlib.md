---
title: Python Module -- hashlib
date: 2025-01-04 15:44
categories: Foundation of programming
tags:
    - "Python"
    - "Python module"
    - "Programe"
excerpt: false
---

## hashlib

哈希函数又称哈希算法或散列函数，是一种为已有的数据创建“数字指纹”（哈希摘要）的方法。哈希函数把数据压缩成摘要，对于相同的输入，哈希函数可以生成相同的摘要（数字指纹），需要注意的是这个过程并不可逆（不能通过摘要计算出输入的内容）。一个优质的哈希函数能够为不同的输入生成不同的摘要，出现哈希冲突（不同的输入产生相同的摘要）的概率极低，[MD5](https://zh.wikipedia.org/wiki/MD5)、[SHA家族]([https://zh.wikipedia.org/wiki/SHA%E5%AE%B6%E6%97%8F](https://zh.wikipedia.org/wiki/SHA家族))就是这类好的哈希函数。

> **说明**：2004年8月，在美国加州圣巴巴拉召开的国际密码大会上，我国王小云宣读了自己和研究团队对于MD4、MD5、HAVAL-128和RIPEMD四个国际著名密码算法的破译结果，导致普遍使用的MD5证书作为校验失去校验效果。在2011年的时候，在RFC 6151中已经禁止将MD5用作密钥散列消息认证码。

Python标准库的`hashlib`模块提供了对哈希函数的封装，通过使用`md5`、`sha1`、`sha256`等类，我们可以轻松的生成“数字指纹”。

```python
import hashlib

# 计算字符串"123456"的MD5摘要
print(hashlib.md5('123456'.encode()).hexdigest())

# 计算文件"Python-3.7.1.tar.xz"的MD5摘要
hasher = hashlib.md5()
with open('Python-3.7.1.tar.xz', 'rb') as file:
    data = file.read(512)
    while data:
        hasher.update(data)
        data = file.read(512)
print(hasher.hexdigest())
```

