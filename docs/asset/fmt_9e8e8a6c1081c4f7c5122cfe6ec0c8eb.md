
返回 `s` 中的元素数量。`s` 应该是列表、元组、字符串。

## 231 内置函数与类型

`list([items])`

表示列表的类型。`items` 是任何可迭代对象，值用于填充列表。如果没有提供参数，返回一个空列表。

`locals()`

返回对应本地命名空间的字典。此字典仅用于检查——修改是不安全的。

`long(x [, base])`

Python 2 中表示整数的类型。如果 `x` 是数字，则会被转换为 `long`。如果 `x` 是字符串，则会被解析为 `long`。如果没有提供参数，此函数返回 `0L`。

`map(function, items, ...)`

在 Python 2 中，这应用于 `items` 的每一个项目并返回结果列表。在 Python 3 中，创建一个产生相同结果的迭代器。如果提供了多个输入序列，假设函数接受任意参数，每个参数从不同的序列中获取。处理多个输入时的行为在 Python 2 和 3 之间不同。结果的长度为最长输入序列，当较短序列耗尽时使用 `None` 作为填充值。在 Python 3 中，结果仅与最短的序列等长。

`max(s [, args, ...])`

对于单个参数 `s`，此函数返回 `s` 中元素的最大值，`s` 可以是任何可迭代的。。对于多个参数，它返回参数中最大的那个。

`min(s [, args, ...])`

对于单个参数 `s`，此函数返回 `s` 中元素的最小值，`s` 可以是任何可迭代的对象。对于多个参数，它返回参数中最小的那个。

`next(s [, default])`

从迭代器 `s` 获取下一个项目。如果迭代器没有更多项目，则会抛出 `StopIteration` 异常，除非为 `default` 参数提供了值。在这种情况下，则返回默认值。为了可移植性，你应该始终使用此函数，而不是直接对迭代器 `s` 调用 `s.next()`。在 Python 3 中，底层方法的名称是 `s.__next__()`。

## 第 12 章 内置函数与异常

`object()`

Python 中所有对象的基类。你可以调用它来创建一个实例，但结果并没有特别有趣。

`oct(x)`

将整数 `x` 转换为八进制字符串。

`open(filename, mode [, bufsize]])`

在 Python 2 中，`open` 打开文件 `filename` 并返回一个新对象（详阅第 9 章“输入与输出”）。`mode` 是一个字符串，指示如何打开文件：'r' 用于读取，'w' 用于写入，'a' 用于追加。第二个字符 't' 或 'b' 用于指示文本模式（默认值）或二进制模式。例如，'r' 或 'rt' 以文本模式打开文件，而 'rb' 以二进制模式打开文件。可以在 `mode` 中添加可选的 'a+' 以进行文件更新（允许同时读取和写入）。'w+' 模式如果文件已存在，则会截断该文件。'a+' 或 'at+' 模式打开文件进行读写，但在打开文件时保持原始内容不变。如果指定了 'u' 或 'ur' 模式，文件将以通用换行模式打开。在这种模式下，所有变体换行符（'\n', '\r', '\r\n'）都会转换为 '\n'。如果省略 `mode`，则 `bufsize` 参数指定行为，其中 0 表示无缓冲，任何其他正数表示字节单位的近似缓冲区大小。负数表示应使用系统默认缓冲（这是默认行为）。

`open(filename, mode [, bufsize], encoding [, errors [, newline [,\nclosedfile]]]])`

在 Python 3 中，这打开 `filename` 并返回一个文件对象。前三个参数的含义与上述 Python 2 版本相同。`encoding` 是编码名称，如 'utf-8'。`errors` 是错误处理策略，为 'strict'、'ignore'、'replace'、'backslashreplace' 或 'xmlcharereplace'之一。`newline` 控制通用换行模式的行为，设置为 None、'\n'、'\r' 或 '\r\n'。`closedfile` 是一个布尔标志，指定在调用 `close()` 方法时文件描述符是否关闭。与 Python 2 不同，返回的对象类型取决于所选的 I/O 模式。如果你以二进制模式打开文件，将得到一个 `read()` 和 `write()` 等 I/O 操作作用字节数组的对象。文件 I/O 是 Python 2 和 3 之间存在显著差异的领域之一。更多细节请附录 A，“Python 3”。

`ord(c)`

返回单个字符 `c` 的数值。对于普通字符，返回范围在 [0, 255] 内的值。对于 Unicode 字符，通常返回范围在 [0, 65535] 内的值。在 Python 3 中，`c` 也可以是 Unicode 代理对，在这种情况下它会被转换为相应的 Unicode 代码点。

`pow(x, y [, z])`

返回 `x ** y`。如果提供了 `z`，此函数返回 `(x ** y) % z`。如果三个参数都给出，它们必须是整数且 `y` 必须为负数。

## 内置函数与类型 209

```python
print(value, ..., sep=separator, end=ending, file=outfile)
```

Python 3 用于打印一系列值的函数。作为输入，你可以提供任意数量的值，所有值都会打印在同一行。`sep` 关键字参数用于指定分隔符字符（默认为空格）。`end` 参数指定不同的行尾符（默认位 '\n'）。`file` 参数将输出重定向到文件对象。如果你在代码中添加 `__future__ import print_function` 语句，则可以在 Python 2 中使用此函数。

```python
property(fget, fset [, fdel], [doc])
```

为类创建属性属性（property）。`fget` 是一个返回属性值的函数，`fset` 用于设置该值，`fdel` 删除属性。`doc` 提供文档字符串。可以使用关键字参数设置参数——例如：`property(fgetX, doc="some text")`。

```python
range([start], stop, [step])
```

在 Python 2 中，这会创建一个从 `start` 到 `stop` 的完整整数列表。如果省略 `step`，则索引设置为 1。如果调用 `range()` 时只有一个参数，则默认为 0。负数 `step` 会创建一个降序排列的数字列表。在 Python 3 中，`range()` 创建一个特殊的 range 对象，它按需计算其值（类似于以前版本中的 `xrange()`）。

```python
raw_input([prompt])
```

Python 2 函数，从输入（`sys.stdin`）读取一行并将其作为字符串返回。如果提供了 `prompt`，它会先打印到标准输出（`sys.stdout`）。末尾换行符会被去除，如果到达 EOF 则会抛出 `EOFError` 异常。如果加载了 `readline` 模块，此函数将提供高级行编辑和命令补全功能。在 Python 3 中使用 `input()` 读取输入。

```python
repr(object)
```

返回对象的字符串表示。在大多数情况下，返回的字符串是一个表达式，可以传递给 `eval()` 来重新创建对象。请注意在 Python 3 中，此函数的结果可能是 Unicode 字符串，无法在终端或 shell 窗口中显示（导致异常）。使用 `ascii()` 函数创建对象的 ASCII 表示。

```python
reversed(s)
```

为序列 `s` 创建一个反向迭代器。此函数仅实现了序列方法 `__len__` 和 `__getitem__`。此外，`s` 必须是从 0 开始索引的项目。

```python
round(x[, n])
```

将浮点数 `x` 四舍五入到 `n` 的倍数。如果省略 `n`，默认为 0。如果两个值足够接近，Python 2 向偶数舍入，Python 3 向远离 0 的方向舍入。

## 第 12 章 内置函数与异常

`set([items])`

创建一个由迭代对象 `items` 填充的集合。`items` 必须是不可变的。如果省略 `items`，则返回一个空集合。

```python
setattr(object, name, value)
```

设置对象的属性。`name` 是字符串。相当于 `object.name = value`。

```python
slice([start[, step])
```

返回一个表示指定范围的 slice 对象。slice 对象通过扩展语法 `a[i:k]` 生成。详情请参见第 3 章“序列与映射方法”。

```python
sorted(iterable[, key=keyfunc, reverse=reverse])
```
