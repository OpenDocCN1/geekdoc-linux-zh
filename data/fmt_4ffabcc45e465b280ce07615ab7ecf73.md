
```python
def loadPickle(self):
    error = None
    fh = None
    try:
        fh = gzip.open(unicode(self.__fname), "rb")
        self.clear(False)
        self.__movies = cPickle.load(fh)
        for key, movie in self.__movies:
            self.__movieFromId[mid(movie)] = movie
    except (IOError, OSError), e:
        error = "Failed to load: %s" % e
    finally:
        if fh is not None:
            fh.close()
        if error is not None:
            return False, error
        self.__dirty = False
        return True, "Loaded %d movie records from %s" % (
            len(self.__movies),
            QFileInfo(self.__fname).fileName())
```

## 反序列化（Unpickling）

反序列化（Unpickling）几乎和序列化一样简单。我们必须记住使用 `gzip` 打开文件，以便对其进行解压。`open()` 的 `rb` 参数表示“以二进制模式读取”。我们使用 `pickle` 的 `load()` 函数来检索数据；它接受一个文件句柄并返回整个数据结构。我们将数据结构直接赋值给我们的 `__movies` 列表。然后我们遍历电影记录以填充 `__movieFromId` 字典。这个字典不能被保存，因为它依赖于 `Movie` 的 `id()`（每次运行应用程序时都会发生变化）。

序列化和反序列化是保存和加载二进制数据最简单的方法，非常适合我们的数据保存在标准 Python 数据类型中的情况。如果我们将数据保存为 PyQt 数据类型，通常最好使用 `QDataStream`。这个类在存储复杂的 PyQt 数据类型（如图像）时比 `pickle` 模块更高效（因为不需要 `pickle` 所需的转换开销），并且它生成的文件比 `pickle` 模块生成的更紧凑（除非 `pickle` 数据被压缩）。它还提供了一种便捷的方式，与 C++/Qt 应用程序实现无缝的数据格式互操作性。

## 保存和加载文本文件

PyQt 和 Python 标准库提供了编写和读取文本文件的设施。PyQt 使用 `QTextStream` 类，而 Python 标准库使用 `codecs` 模块。

纯文本格式通常是人类可读的，例如在文本编辑器中，并且通常易于编写。任何类型的数据都可以通过某种方式写为纯文本。数字和日期可以通过使用它们的字符串表示形式非常轻松且紧凑地写入，而其他类型（如图像）可以以更冗长的形式写入——例如，使用 `.xpm` 格式。

读取包含非上下文数据或具有结构（例如记录结构）的纯文本意味着我们必须编写解析器，这可能相当困难，尤其是对于复杂数据或复杂数据结构。纯文本格式在扩展性方面也可能相当棘手，以保持与早期格式的兼容性，而且由于读取编码和写入编码之间的差异，它们容易因用户可能使用假设了不同编码的文本编辑器进行编辑而导致误读。这些格式对于存储简单数据类型的简单文件结构最为有用。

| 格式 | 示例 |
| :--- | :--- |
| `{{MOVIE}}\n\ttitle\n` | `{{MOVIE}}\t12 Monkeys` |
| `year\n minutes\n acquired\n` | `1995 129 2001-06-21` |
| `\t\t\t(NOTES)\n` | `(NOTES)` |
| `notes\n` | `Based on La Jetée` |
| `{{ENDMOVIE}}\n` | `{{ENDMOVIE}}` |

**图 8.4** My Movies 文本格式

我们需要写入的数据仅包含简单类型：字符串、整型和日期。但我们仍然需要结构化文本文件，以便能够区分每个电影记录，并且我们必须考虑到备注文本可能跨越多行的事实。

我们选择的结构如图 8.4 所示。在左侧的“格式”列中，空格由 `{down}` 表示，换行符由 `{down}` 表示。

备注可以跨越多行，但我们假设没有一行备注以 `{{ENDMOVIE}}` 文本开头。更稳健的解决方案将涉及转义。例如，我们可以假设对于任何以 `\` 开头的行，我们忽略 `\` 并将该行其余部分视为字面文本。这将允许我们通过将其写为 `\\{{ENDMOVIE}}` 来包含一行文本 `{{ENDMOVIE}}`。

### 使用 QTextStream 进行写入和读取

使用 `QTextStream` 写入文本格式的代码与我们使用 `QDataStream` 写入的代码非常相似。

```python
def saveTextStream(self):
    error = None
    fh = None
    try:
        fh = QFile(self.__fname)
        if not fh.open(QIODevice.WriteOnly):
            raise IOError, unicode(fh.errorString())
        stream = QTextStream(fh)
        stream.setCodec(CODEC)
        for key, movie in self.__movies:
            stream << "{{MOVIE}}" << movie.title << "\n" \
            << movie.year << " " << movie.minutes << " " \
            << movie.acquired.toString(Qt.ISODate) \
            << "\n\n(NOTES)"
            if not movie.notes.isEmpty():
                stream << "\n" << movie.notes
            stream << "\n\n{{ENDMOVIE}}\n"
```

有两个关键点需要注意。首先，我们必须指定要使用的编码。我们在所有情况下都使用 UTF-8；（`CODEC` 持有文本 UTF-8）。如果我们不这样做，PyQt 将使用本地 8 位编码，在美国这可能是 ASCII、Latin-1 或 UTF-8，在西欧可能是 Latin-1 或 UTF-8，在日本可能是 EUC-JP、JIS、Shift-JIS 或 UTF-8。通过指定编码，我们确保始终使用指定的编码进行写入和读取，从而避免字符被错误解释。不幸的是，我们无法保证用户使用正确的编码来编辑我们的文本文件。如果文件可能被编辑，我们可以在第一行用 ASCII 写入编码——例如，以类似 XML 的方式写作 `encoding='UTF-8'`——至少为编辑器提供一个提示。随着 UTF-8 成为文本文件编码的事实全球标准，这个问题在未来几年应该会减少。

第二点应该很明显：所有数据必须作为文本写入。`QTextStream` 重载了 `<<` 操作符以自动处理布尔值、数字和 `QString`，但其他数据类型必须转换为它们的字符串表示形式。对于日期，我们选择使用 ISO `YYYY-MM-DD` 格式。我们还选择避免在备注为空时，在 `(NOTES)` 标记后留有空白行。

*如果格式非常简单，使用 `QSettings` 对象并让其读写到指定文件，而不是手写代码，可能是最简便的方法。

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
