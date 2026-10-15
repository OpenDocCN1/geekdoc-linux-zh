
这将使得当你按下 Tab 键时，Python 显示部分输入的函数和变量。

## 16. Python 文档工具

你可以使用命令通过弹出界面搜索 Python 文档：

```python
pysdoc -g
```

## 17. 文档服务器

你可以在本地机器的端口上启动 HTTP 服务器。这将为你提供访问所有 Python 文档的漂亮界面，包括第三方模块文档。

```
pysdoc -p <port>
```

## 18. Python 开发软件

有很多工具可以帮助 Python 开发，这里有几个重要的：

- IDE: Python 是内置的，具有自动补全、函数弹出帮助等。
- PyCharm: 另一个增强型 Python IDE，具有 Tab 补全和其他功能。
- Erici: 一个 GUI IDE，具有自动补全、类浏览器、内置功能和调试器。
- WIDE: 商业级 IDE，为各地的开源开发者提供免费许可。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_66_0.png)

# Python 基础

![](img/3c5b3591dd9ac4cceb489cee11bd7908_67_0.png)

## 内置模块

### 23. Do-while 循环

由于 Python 还没有 do-while 或 do-until 循环（目前），你可以使用以下方法模拟它们的结果：

```python
while True:
    do_something()
    if condition:
        break
```

### 19. 在 Python 解释器运行时执行函数

你可以使用 `eval()` 在 Python 解释器运行时执行函数。

示例：

```python
def sum():
    print(4+5)
def message():
    print("Executing Now")
import atexit
atexit.register(sum)
atexit.register(message)
```

输出：

```text
Executing Now
```

### 24. 检测系统平台

为了使用特定于平台的函数，检测 Python 解释器运行的平台很有用。

示例：

```python
import sys
print(sys.platform)
# MacOS Linux
print(os.release)
```

### 28. 分数数字

`sum()` 返回列表中所有元素的和。`Fraction` 接受一个可选参数：开始和的值。

```python
from operator import itemgetter
Fraction(numerator, denominator)
```

### 29. 数学运算

`math` 模块提供了大量的函数。这些函数作用于整数和浮点数。对于复数，使用 `cmath` 模块。

```python
math.acos(x) : 返回 x 的余弦。
math.factorial(x) : 返回阶乘。
```

### 20. 转换为十六、二进制和八进制

Python 提供了易用的函数将整数转换为十六、二进制和八进制。

示例：

```python
bin(24)
hex(24)
oct(24)
```

### 25. 禁用垃圾回收

有时你可能想要启用或禁用垃圾回收。使用 `gc` 模块启用或禁用。

示例：

```python
gc.enable()
gc.disable()
gc.collect()
```

### 21. 转换为 UTF-8

你可以使用以下函数将任何字符串转换为 UTF-8。

```python
"kunal".encode('utf-8')
```

### 22. 从列表中移除重复

如果你想从列表中移除重复项，使用 `dict()` 然后返回键。

```python
from operator import itemgetter
def dupe(list):
    d = dict(enumerate(list))
    return d.keys()
```

### 26. 使用 C 风格列表提高性能

使用这些列表可以带来显著提升。

示例：

```python
from collections import Counter
c = Counter(string)
```

### 37. 计算可迭代对象的最大值和最小值

你可以使用以下函数找到列表中最大的元素：

```python
max(list)
min(list)
```

### 30. 数组操作

`array` 模块提供了在程序中使用数组的高效方法。`array` 模块定义：一旦创建了数组，就可以插入、删除和访问元素。这里是一些方法：

```python
import array
a = array.array('i')
array.count(x) : 返回 x 出现的次数。
array.index(x) : 返回索引。
array.reverse() : 反转数组顺序。
```

### 31. 排序项

`bisect` 模块允许你保持列表有序。你可以使用它的函数维护一个排序的列表：

```python
bisect.insert(list, item, high)
bisect.insert_left(list, item, low)
```

### 32. 使用正则表达式搜索

`re` 模块使得使用正则表达式搜索变得简单。你可以使用基于正则表达式的表达式。检查以下：

```python
import re
s = "Kunal is bad boy"
if re.search('K', s):
    print('Match') # 字符
if re.search('[A-Z]', s):
    print('Match') # 类
if re.search('[0-9]', s):
    print('Match') # 数字
```

### 34. Python 中的 SQLite 数据库

SQLite 是一种快速且流行的嵌入数据库，因为它不需要配置且性能卓越。你可以使用 `sqlite3` 模块处理 SQLite 数据库。

示例：

```python
import sqlite3
connection = sqlite3.connect('test.db')
cursor = connection.cursor()
cursor.execute('''CREATE TABLE item(id integer primary key, name text, desc text, price real)''')
sqlite3.Cursor object at 0x0000b2de
```

### 33. 使用 bz2 压缩格式

你可以使用 `bz2` 模块使用 bz2 压缩读写数据。

```python
import bz2
bz2.compress(b"for boy")
b'BZh9\x9c\x9d\x48\x5c\x00\x00\x00\x00\x00\x00\x00\x00\xb5\x06\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x000
```

### 35. 使用 zipfile 操作

你可以使用 `zipfile` 模块压缩和解压文件。

```python
import zipfile
zipfile.ZipFile('filename.zip')
```

关闭文件。你必须调用 `close()`，否则你的程序或资源将泄漏。

```python
zipfile.extract(member, path=None)
从压缩包中提取成员。
```

### 36. 使用 Unicode 字符文件名

你可以使用 `glob` 模块在系统中查找匹配模式的文件路径。

```python
示例:
import glob
glob.glob('*.txt')
glob.glob('*.py')
glob.glob('?*')
```

### 37. 执行基础文件操作（复制、删除和重命名）

你可以使用 `shutil` 模块执行高级别的文件操作。该模块适用于普通文件，但不适用于命名管道、块等特殊文件。

```
>>> shutil.copy(src, dst)
将文件复制到 dst 目录。
>>> shutil.copyfile(src, dst)
从 src 复制到 dst。
>>> shutil.move(src, dst)
```
