
```python
a = range(5)           # a = 0,1,2,3,4
b = range(1,8)        # b = 1,2,3,4,5,6,7
c = range(0,14,3)     # c = 0,3,6,9,12
d = range(8,-1)      # d = 8,7,6,5,4,3,2
```

使用 `range()` 的一个注意事项是，在 Python 2 中，它创建的值是一个包含所有整数值的完整列表。在极大的范围内，这可能会无意中消耗内存。因此，在旧的 Python 代码中，你会看到程序员使用替代函数 `xrange()`。例如：

```python
for i in xrange(1000000000):
    # i = 0,1,2,...,999999999
```

由 `xrange()` 创建的对象在请求查询时按需计算它所代表的内容。出于这个原因，它是表示极大量整数范围的首选方式。在 Python 3 中，`xrange()` 函数已重命名为 `range()`，且旧的 `range()` 函数的功能已被移除。

该语句不仅限于整数序列，还可以用于许多种类型的对象，包括字符串、列表、字典和文件。这里有一个示例：

```python
a = "Hello World"
### 打印 a 中的每一个字符
for c in a:
    print c
```

```python
b = ["Dave","Mark","Ann","Phil"]
### 打印列表 b 的成员
for name in b:
    print name
```

```python
c = {'GOOG': 490.10, 'IBM': 91.50, 'AAPL': 123.15}
### 打印字典的所有成员
for key in c:
    print key, c[key]
```

```python
### 打印文件中所有的行
f = open("foo.txt")

for line in f:
    print line,
```

`for` 循环是 Python 最强大的语言特性之一，因为你可以创建自定义的迭代器对象和生成器，为它提供值序列。关于迭代器和生成器的更多细节可以在本章后面部分以及第 6 章“函数与函数式编程”中找到。

## 函数

你定义 `remainder(a,b)` 来创建一个函数，如下所示：

```python
def remainder(a,b):
    q = a // b # 是截断除法
    r = a - q*b
    return r
```

要调用函数，只需使用函数名并传入包裹在括号中的参数即可，例如 `result = remainder(37,15)`。你可以使用元组从函数返回多个值，如下所示：

```python
def divide(a,b):
    q = a // b # 如果 a 和 b 是整数，则 q 是整数
    r = a - q*b
    return (q,r)
```

当在元组中返回多个值时，你可以像这样将结果解包到变量中：

```python
quotient, remainder = divide(1456,33)
```

要为函数参数分配默认值，请使用赋值：

```python
def connect(hostname,port,timeout=300):
    # 函数体
```

当在函数定义中给出默认值时，在随后的函数调用中可以省略它们。当省略时，参数将直接采用默认值。这里有一个示例：

```
connect('www.python.org', 80)
```

你还可以通过使用关键字并任意顺序提供参数来调用函数。然而，这要求你知道函数定义中的参数名称。这里有一个示例：

```python
connect(port=80,hostname="www.python.org")
```

当函数内部创建或赋值变量时，它们的作用域是局部的。也就是说，变量只在函数体内部定义，并在函数返回时被销毁。要从函数内部修改全局变量的值，请如下使用 `global` 语句：

```python
count = 0
def foo():
    global count
    count += 1 # 修改了全局变量 count
```

## 生成器

函数如果使用 `yield` 语句，就可以生成整个结果序列，而不是返回单个值。例如：

任何使用 `yield` 的函数都是生成器。使用 `yield` 的函数在请求查询时按需计算它所代表的内容。出于这个原因，它是表示极大量整数范围的首选方式（注：原文此处有重复）。

该语句不仅限于整数序列，还可以用于许多种类型的对象，包括字符串、列表、字典和文件。这里有一个示例：

```python
a = "Hello World"
### 打印 a 中的每一个字符
for c in a:
    print c
```

```python
b = ["Dave","Mark","Ann","Phil"]
### 打印列表 b 的成员
for name in b:
    print name
```

```python
c = {'GOOG': 490.10, 'IBM': 91.50, 'AAPL': 123.15}
### 打印字典的所有成员
for key in c:
    print key, c[key]
```

```python
### 打印文件中所有的行
f = open("foo.txt")

for line in f:
    print line,
```

`for` 循环是 Python 最强大的语言特性之一，因为你可以创建自定义的迭代器对象和生成器，为它提供值序列。关于迭代器和生成器的更多细节可以在本章后面部分以及第 6 章“函数与函数式编程”中找到。

（注：由于原始文本存在大量重复，以上译文已根据逻辑整合完成完整性翻译）。

```python
## 对象与类
```

```python
### 通过调用 next() 准备所有的匹配器

for m in matchers: m.next()

# 将活跃的日志文件输入到所有匹配器中。注意，为了使之工作，

# Web 服务器必须正在向日志文件写入数据。

wwwlog = tail(open('access-log'))

for line in wwwlog:

  for m in matchers:

    m.send(line) # 将数据发送到每个匹配器协程

```

关于协程的更多细节可以参考第 6 章。

## 对象与类

程序中使用的所有值都是对象。对象由内部数据和执行涉及该数据的各种类型操作的方法组成。在处理如字符串和列表等内置类型时，你已经使用过对象和方法。例如：

```python
items = [37, 42] # 创建一个列表对象

items.append(73) # 调用 append() 方法
```

```python
dir() 函数列出对象上可用的方法，它是交互式实验的有用工具。例如：
>>> items = [37, 42]
>>> dir(items)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', 
 'count', 'extend', 'index', 'insert', 'pop', 
 'remove', 'reverse', 'sort']
```

在检查对象时，你会看到如 `append()` 和 `insert()` 等熟悉的方法。然而，你还会看到始终以双下划开头并结尾的特殊方法。这些方法实现了各种语言操作。例如，`__add__` 实现了 `+` 运算符：

```python
>>> items.__add__(73, 101)
[37, 42, 73, 101]
```

`class` 语句用于定义新类型的对象和面向对象编程。例如，以下类定义了一个具有 `push()`、`pop()` 和 `length()` 操作的简单栈：

```python
class Stack:
  def __init__(self): # 初始化栈
    self.stack = []
  def push(self, object):
    self.stack.append(object)
  def pop(self):
    return self.stack.pop()
  def length(self):
    return len(self.stack)
```
