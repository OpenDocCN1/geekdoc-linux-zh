

我们省略了 `except` 和 `finally` 代码块的代码，因为它们与我们之前见过几次的内容相同——例如在 `saveQDataStream()` 方法中。

虽然以文本格式写入很直接，但读取回去却不那么容易。一方面，我们将不得不以文本形式读取每个整数（年份、分钟数以及获取日期的组成部分），并将它们转换为文本所代表的整数。但主要问题是我们必须正确解析文件，以提取每部电影的记录属性。

处理整数并不太难，因为 `QString` 提供了 `toInt()` 方法；但是该方法返回成功/失败标志，而不是抛出异常，并且每次处理数字时都要检查这一点，意味着我们需要为每个数字编写三行代码而不是一行。因此，我们创建了一个更具 Python 风格的读取整数的包装函数。

```python
def intFromQString(qstr):
    i, ok = qstr.toInt()
    if not ok:
        raise ValueError, unicode(qstr)
    return i
```

该函数简单地调用 `QString.toInt()`，在失败时抛出异常，或在成功时返回整数。

![](img/9bfe0a027fcc8793bb087287001100dd_265_0.png)

要解析我们的电影文本文件，我们将使用有限状态自动机来收集每部电影的数据。解析单部电影的自动机如图 8.5 所示。这意味着在读取每一行之前，我们都期望该行包含特定内容。如果期望未得到满足，我们就会遇到错误；否则，我们读取预期的数据，并为下一行应包含的内容设置期望。

```python
def loadQTextStream(self):
    error = None
    fh = None
    try:
        fh = QFile(self.__fname)
        if not fh.open(QIODevice.ReadOnly):
            raise IOError, unicode(fh.errorString())
        stream = QTextStream(fh)
        stream.setCodec(CODEC)
        self.clear(False)
        lino = 0
```

该方法的开头很熟悉。一旦我们打开了文件，创建了 `QTextStream`，并设置了编解码器，我们就清空现有的电影数据，准备从磁盘读取数据。

对于每部电影，我们首先期望一个“title”行，其中包含 `{MOVIE}`，后跟一个空格和电影标题；然后是一个“numbers”行，包含年份、分钟数和获取日期；接着是一个“notes”行，仅包含 `{NOTES}`；然后是零个或多个注释文本行；最后是一个仅包含 `{ENDMOVIE}` 的“end”行。我们从期望一个“title”行开始。

为了帮助用户找到格式错误，我们在 `lno` 变量中跟踪当前行号，我们将在错误消息中使用它。

我们用来遍历文件的 `while` 循环的主体相当长，因此我们将分部分查看它。

```python
while not stream.atEnd():
    title = year = minutes = acquired = notes = None
    line = stream.readLine()
    lno += 1
    if not line.startsWith("{{MOVIE}}"):
        raise ValueError, "no movie record found"
    else:
        title = line.mid(len("{{MOVIE}}")).trimmed()
```

我们首先将保存一部电影属性的变量初始化为 None，这样很容易判断我们是否读取了所有属性。

我们遍历文件中的每一行。与 Python 标准库的 `file.readline()` 方法不同，PyQt 的 `QTextStream.readLine()` 会去除行尾的换行符。每次读取一行时，我们都递增 `lno`。

我们为任何电影期望的第一行是以 `{MOVIE}` 标记开头的行。如果该行不正确，我们抛出带有错误消息的异常；异常处理程序将在传递给用户的消息中添加行号。如果有一行正确的行，我们通过读取 `{MOVIE}` 标记后跟随的文本来提取电影标题，并去除行首的任何前导和尾部空白。

`QString.mid(n)` 方法相当于 `unicode[n:]`，而 `QString.trimed()` 则等同于 `unicode.strip()`。

现在我们要准备读取“numbers”行。

```python
if stream.atEnd():
    raise ValueError, "premature end of file"
line = stream.readLine()
lno += 1
parts = line.split(" ")
if parts.count() != 3:
    raise ValueError, "invalid numeric data"
```

```python
year = intFromQStr(parts[0])
minutes = intFromQStr(parts[1])
ymd = parts[2].split("-")
if ymd.count() != 3:
    raise ValueError, "invalid acquired date"
acquired = QDate(intFromQStr(ymd[0]),
                 intFromQStr(ymd[1]),
                 intFromQStr(ymd[2]))
```

我们首先检查是否过早达到了文件末尾，如果是，则抛出异常。否则，我们读取“numbers”行。这一行应该有一个整数（年份）、一个空格、一个整数（分钟数）、一个空格，以及 YYYY-MM-DD 格式的获取日期。我们最初按空格字符分割该行，这应该给我们三个字符串：年份、分钟数和获取日期。我们使用我们的 intFromQStr() 函数将文本转换为其代表的整数；如果任何转换失败，都会抛出异常，并由该方法的异常处理程序处理。我们直接转换年份和分钟数，但对于获取日期，我们必须再次分割字符串，这次是按连字符字符，然后使用从每个部分提取的整数值构造一个 QDate。

现在我们要准备读取 {NOTES} 标记，可选地跟随注释行，最后是 {ENDMOVIE} 标记。

```python
if stream.atEnd():
    raise ValueError, "premature end of file"
line = stream.readLine()
line += 1
if line != "{NOTES}":
    raise ValueError, "notes expected"
notes = QString()
while not stream.atEnd():
    line = stream.readLine()
    line += 1
    if line == "{{ENDMOVIE}}":
        if title is None or year is None or \
           minutes is None or acquired is None or \
           notes is None:
            raise ValueError, "incomplete record"
        self.add(Movie(title, year, minutes, \
                       acquired, notes.trimmed()))
        break
    else:
        notes += line + "\n"
else:
    raise ValueError, "missing endmovie marker"
```

### 表 8.2 选定的 QTextStream 方法

| 语法 | 描述 |
| :--- | :--- |
| `s.atEnd()` | 如果已达到 `QTextStream` `s` 的末尾，则返回 `True` |
| `s.setCodec(c)` | 将 `QTextStream` `s` 的文本编解码器设置为 `c` 中指定的编解码器——这可以是字符串（例如，“UTF-8”），或一个 `QTextCodec` 对象 |
| `s << x` | 将对象 `x` 写入 `QTextStream` `s`；`x` 可以是 `bool`、`float`、`int`、`long`、`QString`、`str`、`unicode` 以及少数其他类型 |
| `s.readLine()` | 读取一行，将其作为去除任何行尾字符的 `QString` 返回 |
| `s.readAll()` | 读取整个文件，将其作为 `QString` 返回 |

我们期望得到一行包含 `(NOTES)` 标记。在此时，我们将 notes 变量设置为空的 `QString`。即使没有添加注释文本，拥有一个 `QString` 而不是 `None` 这一事实也足以告诉我们我们读取了注释，即使它们是空的。

现在有两种可能性。要么我们有 `(ENDMOVIE)` 标记，要么我们在读取一行注释。在后一种情况下，我们只需将该行追加到我们目前累积的注释中，并添加回 PyQt 的 `readLine()` 方法去除的换行符。然后我们循环，要么有 `(ENDMOVIE)` 标记，要么有另一行注释。

如果我们得到该标记，我们检查我们的变量中是否有 `None`，以确保我们已读取电影记录的所有数据，然后使用我们收集的数据创建并添加一部新电影。现在我们将退出内部 `while` 循环，准备读取另一部电影，或者如果刚读取的是文件中的最后一部则结束。

如果我们从未得到 `(ENDMOVIE)` 标记，在某个时候会达到文件末尾，内部 `while` 循环将终止。如果发生这种情况，`while` 循环的 `else` 子句将执行并抛出适当的异常。`while` 或 `for` 循环的 `else` 子句仅在循环完成时执行，而不是在循环被 `break` 语句终止时执行。

```python
except (IOError, OSError, ValueError), e:
    error = "Failed to load: %s on line %d" % (e, lineno)
finally:
    if fh is not None:
        fh.close()
    if error is not None:
        return False, error
    self._dirty = False
    return True, "Loaded %d movie records from %s" % (
        len(self._movies),
        QFileinfo(self._fname).fileName())
```

