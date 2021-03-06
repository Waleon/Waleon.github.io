---
layout: post
title: Python 读取大文件
modified: 2018-09-20
categories: Python
tags: 
  - Python
  - 文件 I/O
comments: true
---

# 简述

在处理大数据时，有可能会碰到好几个 G 大小的文件。如果通过一些工具（例如：NotePad++）打开它，会发生错误，无法读取任何内容。

那么，在 Python 中，如何快速地读取这些大文件呢？

<b><font color="LimeGreen">| </font></b><font size = "2" color="#858585">版权声明：一去、二三里，未经博主允许不得转载。</font>

# 一般的读取

读取文件，最常见的方式是：

```Python
with open('filename', 'r', encoding = 'utf-8') as f:
    for line in f.readlines():
        do_something(line)
```

但是，当完成这一操作时，`readlines()` 方法（`read()` 也一样）会将整个文件加载到内存中。在文件较大时，往往会引发 `MemoryError`（内存溢出）。

那么，如何避免这个问题？

# 使用 fileinput 模块

稍微好点儿的方式是使用 `fileinput` 模块：

```Python
import fileinput

for line in fileinput.input(['filename']):
    do_something(line)
```

调用 `fileinput.input()` 会按照顺序读取行，但是在读取之后不会将它们保留在内存中。

# 逐行读取

除此之外，也可使用 `while()` 循环和 `readline()` 来逐行读取：

```Python
with open('filename', 'r', encoding = 'utf-8') as f:
    while True:
        line = f.readline()  # 逐行读取
        if not line:  # 到 EOF，返回空字符串，则终止循环
            break
        do_something(line)
```

# 指定每次读取的长度

有时，可能希望对每次读取的内容进行更细粒度的控制。

在这种情况下，可以使用 `iter` 和 `yield`：

```Python
def read_in_chunks(file_obj, chunk_size = 2048):
    """
    逐件读取文件
    默认块大小：2KB
    """
    while True:
        data = file_obj.read(chunk_size)  # 每次读取指定的长度
        if not data:
            break
        yield data

with open('filename', 'r', encoding = 'utf-8') as f:
    for chuck in read_in_chunks(f):
        do_something(chunk)
```

# 自动管理

这才是 `Pythonci` 最完美的方式，既高效又快速：

```Python
with open('filename', 'r', encoding = 'utf-8') as f:
    for line in f:
        do_something(line)
```

`with` 语句句柄负责打开和关闭文件（包括在内部块中引发异常时），`for line in f` 将文件对象 `f` 视为一个可迭代的数据类型，会自动使用 `IO` 缓存和内存管理，这样就不必担心大文件了。

# 更多参考

- [How to read large file, line by line in python](https://stackoverflow.com/questions/8009882/how-to-read-large-file-line-by-line-in-python "How to read large file, line by line in python")