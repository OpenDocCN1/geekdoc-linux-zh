
在 Python 3.0 之前，字符串字符以其 ASCII 数值代码值存储在 0-127 的范围内，仅代表无重音的拉丁字符。例如，小写字母 'a' 被分配 97 作为其代码值。实际上，计算机内存的每个字节可以存储 0-255 范围内的值，但这仍然太有限，无法表示所有带重音字符和非拉丁字符。例如，西欧使用的带重音字符和用于俄语的西里尔字母无法在 128-255 范围内表示，因为有超过 127 个这样的字符。Python 的最近版本通过存储字符串字符为其 Unicode 码点值来克服这一限制，以在 0-1,114,111 的数字范围内表示所有字符和字母表。高于 ASCII 范围的字符可能需要两个字节来表示其码点值，例如 'Ö' 的十六进制 `0xC3 0xB6`。

`str` 对象的 `encode()` 方法可用于从默认 Unicode 编码进行转换，其 `decode()` 方法可用于转换回 Unicode 默认编码。

Python 的 "`unicodedata`" 模块有用地提供了一个 `name()` 方法，可揭示每个字符的 Unicode 名称。带重音和非拉丁字符可以通过其 Unicode 名称或解码其 Unicode 十六进制码点值来引用。

![](img/d06b1f1cf83677f6647237f0c7827141_158_0.png)

术语 “ASCII” 是 American Standard Code for Information Interchange（美国信息交换标准代码）的首字母缩写。

### 练习步骤

1. 通过用一个包含非 ASCII 字符的字符串初始化一个变量来开始一个新的 Python 脚本，然后显示其值、数据类型和字符串长度

```python
s = 'Röd'
print('\nRed String:', s)
print('Type:', type(s), 'Length:', len(s))
```

![](img/d06b1f1cf83677f6647237f0c7827141_159_0.png)

2. 接下来，编码该字符串，并再次显示其值、数据类型和字符串长度

```python
s = s.encode('utf-8')
print('\nEncoded String:', s)
print('Type:', type(s), 'Length:', len(s))
```

3. 现在，解码该字符串，并再次显示其值、数据类型和字符串长度 — 以揭示非 ASCII 字符的十六进制码点

```python
s = s.decode('utf-8')
print('\nDecoded String:', s)
print('Type:', type(s), 'Length:', len(s))
```

4. 然后，添加语句以使 “unicodedata” 功能可用，并添加一个循环来揭示字符串中每个字符的 Unicode 名称

```python
import unicodedata
for i in range(len(s)):
    print(s[i], unicodedata.name(s[i]), sep=':')
```

5. 接下来，添加语句将变量分配一个包含非 ASCII 字符十六进制码点的新值，然后显示解码的字符串值

```python
s = b'Gr\xc3\xb6n'
print('\nGreen String:', s.decode('utf-8'))
```

6. 最后，添加语句将变量分配另一个包含非 ASCII 字符 Unicode 名称的新值，然后显示字符串值

```python
s = 'Gr\N{LATIN SMALL LETTER O WITH DIAERESIS}n'
print('Green String:', s)
```

7. 将文件保存在你的 scripts 目录中，然后在那里打开一个命令提示符窗口并运行此程序 — 以查看转换的字符串和 unicode 字符名称

`C:\MyScripts>python unicode.py`

红色字符串：Röd

类型：<class 'str'>       长度：3

编码后的字符串：b'R\xc3\xb6d'

类型：<class 'bytes'>     长度：4

解码后的字符串：Röd

类型：<class 'str'>       长度：3

R : 拉丁字母大写 R

ö : 带分音符的大写拉丁字母 O

d : 拉丁字母小写 d

绿色字符串：Grön

绿色字符串：Grön

`C:\MyScripts>`

![](img/d06b1f1cf83677f6647237f0c7827141_160_0.png)

包含字节地址的字符串必须在前面立即加上 `b`，以表示该字符串是字节字面量。

![](img/d06b1f1cf83677f6647237f0c7827141_160_1.png)

在此表示格式中，Unicode 名称均为大写，并通过在 `{ }` 花括号中包含该名称，并在前面加上 `\N` 来引用。

### 访问文件

可以使用 `dir()` 函数检查 `__builtins__` 模块，以揭示其中包含一个文件对象，该对象定义了几种用于处理文件的方法，包括 `open()`、`read()`、`write()` 和 `close()`。

在读取或写入文件之前，必须首先使用 `open()` 方法打开该文件。这需要两个字符串参数来指定文件的名称和位置，以及以下“模式”说明符之一，用于指定打开文件的方式：

| 文件模式： | 操作： |
| :---: | :--- |
| `r` | 打开现有文件以读取 |
| `w` | 打开现有文件以写入。如果文件不存在则创建新文件，或者打开现有文件并丢弃其所有先前内容 |
| `a` | 追加文本。在文件末尾打开或创建一个文本文件用于写入 |
| `r+` | 打开文本文件以读取或写入 |
| `w+` | 打开文本文件以写入或读取 |
| `a+` | 在文件末尾打开或创建文本文件以读取或写入 |

如果模式在上述列出的任何文件模式后包含 `b`，则该操作针对的是二进制文件而非文本文件。例如，`rb` 或 `w+b`

一旦文件被打开并且你拥有一个文件对象，你就可以从其属性中获取与该文件相关的各种详细信息：

| 属性： | 描述： |
| :---: | :--- |
| `name` | 已打开文件的名称 |
| `mode` | 文件打开时的模式 |
| `closed` | 表示 `True` 或 `False` 的状态布尔值 |
| `readable()` | 表示 `True` 或 `False` 的读取权限布尔值 |
| `writable()` | 表示 `True` 或 `False` 的写入权限布尔值 |

![](img/d06b1f1cf83677f6647237f0c7827141_162_0.png)

文件模式参数是字符串值，因此必须用引号包围。

![](img/d06b1f1cf83677f6647237f0c7827141_162_1.png)

你也可以使用 `readlines()` 方法，该方法返回所有行的列表。

- 通过为名为“example.txt”的新文本文件创建一个文件对象以写入内容，从而开始编写一个新的 Python 脚本

```python
file = open( 'example.txt' , 'w' )
```

![](img/d06b1f1cf83677f6647237f0c7827141_162_2.png)

- 接下来，添加语句以显示文件名和模式

```python
print( 'File Name:' , file.name )
print( 'File Open Mode:' , file.mode )
```

- 现在，添加语句以显示文件访问权限

```python
print( 'Readable:' , file.readable() )
print( 'Writable:' , file.writable() )
```

- 然后，定义一个函数来确定文件的状态

```python
def get_status( f ) :
    if ( f.closed != False ) :
        return 'Closed'
    else :
        return 'Open'
```

- 最后，添加语句以显示当前文件状态，然后关闭文件并再次显示文件状态

```python
print( 'File Status:' , get_status( file ) )
```

```python
file.close()
print('\nFile Status:', get_status( file ) )
```

**6**
