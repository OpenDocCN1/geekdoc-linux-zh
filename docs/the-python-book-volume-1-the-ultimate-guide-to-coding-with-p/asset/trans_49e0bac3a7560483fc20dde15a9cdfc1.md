

## 内置模块

### 19. 在 Python 解释器终止时执行函数

你可以使用 `atexit` 模块在 Python 解释器终止时执行函数。

# 示例：

```
def sum():
    print(4+5)
def message():
    print("Executing Now")
import atexit
atexit.register(sum)
atexit.register(message)
```

# 输出：

Executing Now
9

### 20. 从整数转换为二进制、十六进制和八进制

Python 提供了易用的函数——`bin()`、`hex()` 和 `oct()`——分别用于将整数转换为二进制、十进制和八进制格式。

# 示例：

```
>>> bin(24)
'0b11000'
>>> hex(24)
'0x18'
>>> oct(24)
'0o30'
```

### 21. 将任意字符集转换为 UTF-8

你可以使用以下函数将任意字符集转换为 UTF-8。

```
data.decode("input_charset_here").encode('utf-8')
```

### 22. 从列表中去除重复项

如果你想去除列表中的重复项，只需将每个元素作为键放入字典中（例如值设为 `none`），然后检查 `dict.keys()`。

```
from operator import setitem
def distinct(l):
    d = {}
    map(setitem, (d,)*len(l), l, [])
    return d.keys()
```

### 23. Do-while 循环

由于 Python（尚）没有 do-while 或 do-until 循环结构，你可以使用以下方法实现类似效果：

```
while True:
    do_something()
    if condition():
        break
```

### 24. 检测系统平台

为了执行特定于平台的函数，检测 Python 解释器所运行的系统平台非常有用。你可以使用 `sys.platform` 来找出当前平台。

# 示例：

```
在 Ubuntu Linux 上
>>> import sys
>>> sys.platform
'linux2'
在 Mac OS X Snow Leopard 上
>>> import sys
>>> sys.platform
'darwin'
```

### 25. 禁用和启用垃圾回收

有时你可能希望在运行时启用或禁用垃圾回收器。你可以使用 `gc` 模块来启用或禁用垃圾回收。

```
>>> import gc
>>> gc.enable()
<built-in function enable>
>>> gc.disable()
<built-in function disable>
```

### 26. 使用基于 C 的模块以获得更好的性能

许多 Python 模块都配有对应的 C 模块。在复杂应用中使用这些 C 模块将带来显著的性能提升。

# 示例：

用 cPickle 代替 Pickle，用 cStringIO 代替 StringIO

### 27. 计算任何列表或可迭代对象的最大值、最小值和总和

你可以使用以下内置函数：

max：返回列表中的最大元素。
min：返回列表中的最小元素。
sum：此函数返回列表中所有元素的总和。它接受一个可选的第二个参数：求和时起始值（默认为 0）。

### 28. 表示分数

可以使用以下构造函数创建 Fraction 实例：

```
Fraction([numerator [, denominator]])
```

### 29. 执行数学运算

`math` 模块提供了大量数学函数。这些函数适用于整数和浮点数，但不适用于复数。对于复数，需要使用单独的模块，称为 `cmath`。

# 例如：

```
math.acos(x): 返回 x 的反余弦值。
math.cos(x): 返回 x 的余弦值。
math.factorial(x): 返回 x 的阶乘。
```

### 30. 使用数组

`array` 模块提供了一种在你的程序中使用数组的高效方式。`array` 模块定义了以下类型：

```
array[typecode [, initializer]]
```

一旦你创建了一个数组对象（比如 myarray），你就可以对其应用许多方法。以下是几个重要的方法：

myarray.count(x)：返回 x 在 a 中出现的次数。
myarray.extend(x)：将 x 追加到数组末尾。
myarray.reverse()：反转数组的顺序。

### 31. 排序项目

`bisect` 模块使得以任意可能顺序维护列表变得非常容易。你可以使用以下函数来对列表排序。

```
bisect.insort(list, item [, low [, high]])
```

将 item 按排序顺序插入到 list 中。如果 item 已经存在于列表中，则新条目插入到任何现有条目的右侧。

```
bisect.insort_left(list, item [, low [, high]])
```

将 item 按排序顺序插入到 list 中。如果 item 已经存在于列表中，则新条目插入到任何现有条目的左侧。

