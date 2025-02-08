---
title: Document reading and writing
date: 2025-01-04 13:44
categories: Foundation of programming
tags:
    - "Python"
    - "Programe"
excerpt: false
---

## 文件读写

使用Python内置的`open`函数来打开文件，在使用`open`函数时，我们可以通过函数的参数指定**文件名**、**操作模式**和**字符编码**等信息。

| 操作模式 | 具体含义                         |
| -------- | -------------------------------- |
| `'r'`    | 读取 （默认）                    |
| `'w'`    | 写入（会先截断之前的内容）       |
| `'x'`    | 写入，如果文件已经存在会产生异常 |
| `'a'`    | 追加，将内容写入到已有文件的末尾 |
| `'b'`    | 二进制模式                       |
| `'t'`    | 文本模式（默认）                 |
| `'+'`    | 更新（既可以读又可以写）         |

### 文本文件

#### 读

```python
def main():
    f = None
    try:
        f = open('文件路径', 'r', encoding='utf-8')
        print(f.read())
    except FileNotFoundError:
        print('无法打开指定的文件!')
    except LookupError:
        print('指定了未知的编码!')
    except UnicodeDecodeError:
        print('读取文件时解码错误!')
    finally:
        if f:
            f.close() # 及时释放资源


if __name__ == '__main__':
    main()
```

遇到文件太大，瞬间占满内存。可以一次读取小部份，读取全部文件

f.read(32)：

* 每次调用时，读取**从当前文件指针位置开始的 32 个字符**。
* 文件指针在读取后会向前移动 32 个字符。
* 当文件指针移动到文件末尾时，f.read(32) 会返回一个**空字符串**（''），这会让 while data: 条件变为 False，从而结束循环。

```python
def main():
    f = None
    try:
        f = open('文件路径', 'r', encoding='utf-8')
        data = (f.read(32))
        while data:
          print(data, end = '')
          data = (f.read(32))
    except FileNotFoundError:
        print('无法打开指定的文件!')
    except LookupError:
        print('指定了未知的编码!')
    except UnicodeDecodeError:
        print('读取文件时解码错误!')
    finally:
        if f:
            f.close() # 及时释放资源


if __name__ == '__main__':
    main()
```

一行一行的读取文件也可以解决一下读取一个很大文件导致内存占满的问题

* `.redalines`把每一行读取作为字符串，所有字符串作为列表
* `.redaline()`只读每一行，每一行为一个字符串.
* `.split()`以空格拆分（可以用“，”指定拆分元素），之后使用列表储存

```python
with open('document.txt') as file:
  no, temp = file.readline().split()
```



### 写

`w`模式，如果文件不存在就会创建这个文件。如果文件存在写入就会覆盖内容，不想覆盖的话使用`a`

```python
with open('test', 'w', encoding='utf-8') as f
    f.write('123\r\n')
    f.write('abc\r\n')

    
with open('test', 'a', encoding='utf-8') as f1
    f1.write('哈哈哈\r\n')
    f1.write('追加\r\n')

```

### 二进制文件

复制文件

```python
def file_copy(source_file, tarrget_file):
    with open(source_file, 'rb') as f_in:
        with open(tarrget_file, 'wb') as f_out:
            data = f_in.read(512)
            while data:
                f_out.write(data)
                data = f_in.read(512)

if __name__ == '__main__':
    file_copy('test8.py', 'test9.py')
```

