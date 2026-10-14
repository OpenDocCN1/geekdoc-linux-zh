
```python
while True:
    do_something()
    if condition():
        break
```

### 24 检测系统平台

为了执行平台特定的功能，检测 Python 解释器正在运行的平台非常有用。你可以使用 `sys.platform` 来查找当前平台。

**示例：**

**在 Ubuntu Linux 上**

```python
>>> import sys
>>> sys.platform
'linux2'
```

**在 Mac OS X Snow Leopard 上**

```python
>>> import sys
>>> sys.platform
'darwin'
```

### 25 禁用和启用垃圾回收

有时你可能想在运行时启用或禁用垃圾回收器。你可以使用 `gc` 模块来启用或禁用垃圾回收。

**示例：**

```python
>>> import gc
>>> gc.enable()
<builtin-function enable>
>>> gc.disable()
<builtin-function disable>
```

### 26 使用基于 C 的模块以获得更好的性能

许多 Python 模块都附带了相应的 C 模块。使用这些 C 模块在复杂应用中会显著提升性能。

**示例：**

使用 `CPickle` 代替 `Pickle`，使用 `cStringIO` 代替 `StringIO`。

### 27 计算任意列表或可迭代对象的最大值、最小值和总和

你可以使用以下内置函数。

- `max`：返回列表中的最大元素。
- `min`：返回列表中的最小元素。
- `sum`：此函数返回列表中所有元素的总和。它接受一个可选的第二个参数：求和时的起始值（默认为 `0`）。

### 28 表示分数

可以使用以下构造函数创建 `Fraction` 实例：

```python
Fraction([numerator [, [denominator]]])
```

### 29 执行数学运算

这些操作适用于整数和浮点数，但不适用于复数。对于复数，使用一个单独的模块，称为 `cmath`。

**例如：**

```python
math.acos(x): Return arc cosine of x.
math.cos(x): Return cosine of x.
math.factorial(x) : Returns x factorial.
```

### 30 处理数组

`array` 模块提供了一种在程序中使用数组的高效方式。`array` 模块定义了以下类型：

```python
array(typecode [, initializer])
```

一旦你创建了一个数组对象，比如 `myarray`，你可以对其应用许多方法。以下是其中几个重要的：

- `myarray.count(x)`：返回 `x` 在 `a` 中出现的次数。
- `myarray.extend(x)`：在数组末尾追加 `x`。
- `myarray.reverse()`：反转数组的顺序。

### 31 对项进行排序

以下函数对列表进行排序。

```python
bisect.insert(list, item [, low [, high]])
```

将 `item` 以排序顺序插入列表。如果 `item` 已经在列表中，新条目将插入到任何现有条目的右侧。

```python
bisect.insort_left(list, item [, low [, high]])
```

将 `item` 以排序顺序插入列表。如果 `item` 已经在列表中，新条目将插入到任何现有条目的左侧。

### 32 使用基于正则表达式的搜索

你可以使用 `re.search()` 函数配合基于正则表达式的模式。请查看下面的示例。

```python
>>> import re
>>> s = "Kunal is a bad boy"
>>> if re.search("K", s): print "Match!" # char literal
Match!
>>> if re.search("[A-Z]", s): print "Match!" # char class
# match either at-sign or capital letter
Match!
>>> if re.search("\d", s): print "Match!" # digits class
```

### 33 处理 bzip2 (.bz2) 压缩格式

你可以使用 `bz2` 模块通过 bzip2 压缩算法来读取和写入数据。

- `bz2.compress()`：用于 bz2 压缩
- `bz2.decompress()`：用于 bz2 解压缩

```python
# File: bz2-example.py
import bz2
MESSAGE = "Kunal is a bad boy"
compressed_message = bz2.compress(MESSAGE)
decompressed_message = bz2.decompress(compressed_message)
print "original:", repr(MESSAGE)
print "compressed message:", repr(compressed_message)
print "decompressed message:", repr(decompressed_message)

# Output:
# [~/src/python $:] python bz2-example.py
# original: 'Kunal is a bad boy'
# compressed message: 'Bzh1A\x83Y\xc4\x6f\x9b\x00\x00\x02\x15\x00e\x00\n\x80\x84\x8a \x00\n\x00\x0c\x84\r\n\x83\c\x2\x0\x8\xdf\x5\x9b\x19\x80\n\xf8\x00\xd9\xc2\xc2\xd4\x86\x0\x86 z\xc\xe0\'
# decompressed message: 'Kunal is a bad boy'
```

### 34 在 Python 中使用 SQLite 数据库

由于 SQLite 无需任何配置且性能卓越，它正迅速成为非常流行的嵌入式数据库。你可以使用 `sqlite3` 模块来操作 SQLite 数据库。

```python
>>> import sqlite3
>>> connection = sqlite3.connect("test.db")
>>> curs = connection.cursor()
>>> curs.execute("""create table item
... (id integer primary key, itemno
... text unique,
... scandesc text, descr text, price
... real)""")
<sqlite3.Cursor object at 0x1004a2b30>
```

### 35 处理 zip 文件

你可以使用 `zipfile` 模块来处理 zip 文件。

- `zipfile.ZipFile(filename [, mode [, compression [, allowZip64]]])`：打开一个 zip 文件，该文件可以是文件路径（字符串）或类文件对象。
- `zipfile.close()`：关闭归档文件。在退出程序之前必须调用 `close()`，否则关键记录可能不会被写入。
- `zipfile.extract(member [, path [, pwd]])`：将归档文件中的成员提取到当前工作目录。`member` 必须是其完整名称（或 zinfo 对象）。`path` 指定提取到的不同目录。`member` 可以是文件名或 zinfo 对象。`pwd` 是用于加密文件的密码。

### 36 使用 UNIX 风格通配符搜索文件名

你可以使用 `glob` 模块根据 UNIX shell 使用的规则来查找所有匹配模式的路径名。`*`、`?` 以及用 `[]` 表示的字符范围将会被匹配。

```python
>>> import glob
>>> glob.glob('[/.0-9]_*.*)'
['/1.gif', '/2.txt']
>>> glob.glob('*.gif')
['1.gif', 'card.gif']
>>> glob.glob('?.gif')
['1.gif']
```

### 37 执行基本文件操作（复制、删除和重命名）

你可以使用 `shutil` 模块在高级别执行基本文件操作。该模块适用于普通文件，因此不适用于命名管道、块设备等特殊文件。

- `shutil.copy(src, dst)`：将文件 `src` 复制到文件或目录 `dst`。
- `shutil.copyfile(src, dst)`：从 `src` 复制文件权限到 `dst`。
