
这会产生以下输出：

亲爱的 Bush 先生，

请退还我的搅拌机或支付我 50.00 美元。
诚挚地，

Joe Python User

`format()` 方法是一种更现代的替代方案，它精简了之前的一些代码。例如：

```python
form = """

Dear {name},

Please send back my {item} or pay me {amount:0.2f}.

Sincerely yours,

Joe Python User
```
对于某些类型的字符串，你也可以像下面一样使用模板字符串（Template strings）：

```python
import string

form = string.Template("""

Dear $name,

Please send back my $item or pay me $amount.

Sincerely yours,

Joe Python User""")
```

```python
print form.substitute({'name': 'Mr. Bush',
    'item': 'blender',
    'amount': "%0.2f" % 50.00})
```

在这种情况下，字符串中的变量表示替换。`form.substitute()` 接收一个替换字典并返回一个新字符串。虽然之前的方法很简单，但它们并不总是文本生成的强力解决方案。Web 框架和其他大型应用框架倾向于提供自己的模板字符串，这些字符串支持嵌入的控制流、变量、函数和高级功能。

# 生成输出

直接与文件交互是程序员最熟悉的 I/O 模型。然而，生成器函数（generator functions）也可以用于以数据片段序列发射 I/O 流。要做到这一点，只需像使用 `write()` 或 `print` 语句一样使用 `yield` 语句即可。这里有一个示例：

## Unicode 字符串处理

```python
def countdown(n):
    while n > 0:
        yield "T-minus %d\n" % n
        n -= 1
    yield "Kaboom!\n"
```

以这种方式产生输出流提供了极大的灵活性，因为输出流的产生与将流引导至预期目的地的代码解耦了。例如，如果你想将输出路由到文件 `f`，你可以这样做：

```python
count = countdown(5)
f.writelines(count)
```

如果，且你想将输出重定向到套接字 `s`，你可以这样做：

```python
for chunk in count:
    s.sendall(chunk)
```

或者，如果你只是想在字符串中捕获所有输出，你可以这样做：

```python
out = ''.join(count)
```

更高级的应用可以使用这种方法来实现它们的 I/O 缓冲（buffering）。例如，生成器可以发射小的片段，但另一个函数可以将片段收集到大缓冲区中，以创建一个更大、更高效的 I/O 操作：

```python
chunks = []
buffered_size = 0
for chunk in count:
    chunks.append(chunk)
    buffered_size += len(chunk)
    if buffered_size >= MAX_BUFFER:
        out.write("".join(chunks))
        chunks.clear()
        buffered_size = 0
```

```python
out.write("".join(chunks))
```

对于将输出路由到文件或网络连接的程序，生成器方法还可以减少内存消耗，因为整个输出流可以以小片段的形式生成并处理，而不是首先收集成一个大输出字符串或字符串列表。这种方法在编写与 Python Web 网关接口 (WSGI) 交互的程序时常见，WSGI 用于在某些 Web 框架的组件之间通信。

# Unicode 字符串处理

与 I/O 处理相关的一个常见问题是字符以 Unicode 形式表示。如果你有一个包含 Unicode 字符串编码表示的原始字节字符串 `s`，请使用 `s.decode([encoding, errors])` 将其转换为适当的字符串。要将 Unicode 字符串编码为字节字符串，使用 `u.encode([encoding, errors])` 方法。这两个转换操作符都要求使用特殊的编码名称，该名称指定了如何将 Unicode 字符值映射到字节字符串中的 8 位字符，反之亦然。`encoding` 参数是一个字符串，是百百多种不同字符编码之一。然而，以下值最常见：

| 值 | 描述 |
| :--- | :--- |
| 'ascii' | 7 位 ASCII |
| 'latin-1' 或 'iso-8859-1' | ISO8859-1 |
| 'cp1252' | Windows1252 编码 |
| 'utf-8' | 8 位变长编码 |
| 'utf-16' | 16 位变长编码（可能是小端序或大端序） |
| 'utf-16-le' | UTF-16 小端序编码 |
| 'utf-16-be' | UTF-16 大端序编码 |
| 'unicode-escape' | 与 Unicode 字面量格式相同 |
| 'raw-unicode-escape' | 与原始字符串格式相同 |

默认编码位于 `site` 模块中，可以通过 `sys.getdefaultencoding()` 查询。在许多情况下，默认编码是 'ascii'，这意味着取值在 [U+0000, U+00FF] 范围内的字符直接映射到 Unicode 字符。然而，'utf-8' 是最常见的。

在处理 Unicode 时，无法直接将原始 Unicode 数据写入文件，因为 Unicode 字符被表示为多字节整数，将此类整数写入输出流会导致与字节序有关。例如，你必须决定 Unicode 字符是以小端序还是大端序表示。此外，处理 Unicode 的其他工具必须知道你是如何编码它们的。由于这个问题，Unicode 字符串的外部表示总是根据特定的编码规则进行的，该规则定义了如何将 Unicode 字符表示为字节序列。因此为了支持 Unicode I/O，上一节描述的编码和解码概念扩展到了文件。内置的 `codecs` 模块包含一组用于将字节数据从 Unicode 字符串转换为各种编码方案的函数。

处理 Unicode 文件最直接的方法是使用 `codecs.open(file, mode, encoding, errors)` 函数，如下：

```python
f = codecs.open('f.txt', 'r', 'utf-8', 'strict') # 读取
g = codecs.open('bar.txt', 'w', 'utf-8') # 写入
```

这创建了一个读取或写入 Unicode 字符串的文件。`encoding` 参数指定了在读取或写入文件时使用的字符编码。`errors` 参数决定如何处理错误，它是上一节描述的 'strict'、'ignore'、'replace'、'backslashreplace' 或 'xmlcharreplace' 之一。

如果你已经有一个文件对象，可以使用 `codecs.EncodedFile(file, inputenc [,])` 函数在其周围放置编码包装。示例如下：

```python
f = open('f.txt', 'rb')
...
enc = codecs.EncodedFile(f, 'utf-8')
```
