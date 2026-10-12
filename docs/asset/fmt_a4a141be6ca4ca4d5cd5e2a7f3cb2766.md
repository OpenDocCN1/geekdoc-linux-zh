
省略号代表为节省空间而被省略的电影记录，它们不是格式的一部分。虽然我们总是以相同的顺序编写 `<movies>` 标签的属性，但对 XML 解析器来说，顺序是任意的。属性值不应包含单引号或双引号，或者 XML 元字符 `<`、`>` 或 `&`。这意味着对于属性值，我们要么转义它们，要么确保仅使用已知不包含这些字符的值——例如，数字、ISO 格式的日期和时间以及布尔值。对于字符数据，如标题和备注，我们可以包含引号，因为只禁止使用元字符。

> 要转义 XML 文本，我们必须将 `<` 转换为 `&lt;`，`>` 转换为 `&gt;`，`&` 转换为 `&amp;`。在属性值中，除了这些转换外，我们还必须将 `"` 转换为 `&quot;`。

```python
def exportXml(self, fname):
    error = None
    fh = None
    try:
        fh = QFile(fname)
        if not fh.open(QIODevice.WriteOnly):
            raise IOError, unicode(fh.errorString())
        stream = QTextStream(fh)
        stream.setCodec(CODEC)
        stream << ('<"xml version=\'1.0\' encoding=\'%s\'>\n'
                "<!DOCTYPE MOVIES>\n"
                "<MOVIES VERSION=\'1.0\'>\n") % CODEC)
```

![](img/9bfe0a027fcc8793bb087287001100dd_272_0.png)

我们选择使用 PyQt 的 `QTextStream` 来编写 XML 文件；我们同样可以轻松使用 `codecs` 模块，尽管在那种情况下我们需要将 `QString` 转换为 Unicode。*

该方法以我们熟悉的方式开始。一旦创建 `QTextStream`，我们像往常一样将其编码设置为 UTF-8，然后输出前三行——这些总是相同的。

```python
for key, movie in self.__movies:
    stream << ("<MOVIE YEAR='%d' MINUTES='%d' "
            "ACQUIRED='%s'>\n") % (
        movie.year, movie.minutes,
        movie.acquired.toString(Qt.ISODate))
    stream << "<TITLE>" << QString(movie.title) \
    << "</TITLE>\n<NOTES>"
    if not movie.notes.isEmpty():
        stream << "\n" << Qt.escape(
            encodedNewLines(movie.notes))
    stream << "\n</NOTES>\n</MOVIE>\n"
stream << "</MOVIES>\n"
```

我们以与之前相同的方式遍历电影数据。`Qt.escape()` 函数接受一个 `QString` 并返回正确转义了任何 XML 元字符的 `QString`。我们使用 `encodedNewLines()` 函数将备注中的任何段落和换行符转换为它们的 Unicode 等价物。我们不对属性进行转义，因为我们知道它们不能包含任何不可接受的字符。我们省略了该方法的结尾部分，因为异常处理和返回在结构上与我们之前看到的相同。

> PyQt 4.0 存在一个 bug，导致 `QTextStream` 无法正确写入，因此在 PyQt 4.0 中我们必须使用 `codecs` 模块。这个问题在 PyQt 4.1 及更高版本中不存在。

### 使用 PyQt 的 DOM 类读取和解析 XML

PyQt 的 `QDomDocument` 类可以一次性读入一个完整的（格式良好的）XML 文档。但一旦我们拥有了一个 `QDomDocument`，就必须知道如何使用它。有些应用会将文档映射到某个控件中，通常是一个 `QTreeWidget`；而像 My Movies 这样的其他应用，将 XML 纯粹用作数据交换格式，它们会遍历文档，并在遍历过程中填充其数据结构。

```python
def importDOM(self, fname):
    dom = QDomDocument()
    error = None
    fh = None
    try:
        fh = QFile(fname)
        if not fh.open(QIODevice.ReadOnly):
            raise IOError, unicode(fh.errorString())
        if not dom.setContent(fh):
            raise ValueError, "could not parse XML"
    except (IOError, OSError, ValueError), e:
        error = "Failed to import: %s" % e
    finally:
        if fh is not None:
            fh.close()
            if error is not None:
                return False, error
    try:
        self.populateFromDOM(dom)
    except ValueError, e:
        return False, "Failed to import: %s" % e
    self.__fname = QString()
    self.__dirty = True
    return True, "Imported %d movie records from %s" % (
        len(self.__movies), QFileInfo(fname).fileName())
```

加载方法的第一部分应该看起来很熟悉，但请注意，当我们调用 `QDomDocument.setContent()` 时，整个文件都会被读取。如果该方法成功（返回 True），我们就知道 XML 已成功解析。

一旦我们拥有了一个 `QDomDocument`，就需要从中提取数据，这正是 `populateFromDOM()` 方法所做的事情。

该方法的结尾与我们之前看到的有所不同。我们清除文件名并将 `dirty` 标志设置为 True。这将确保如果用户尝试保存刚刚导入的 XML 电影数据，或者尝试退出应用程序，他们将获得一个“另存为”对话框，从而有机会将数据保存为应用程序的二进制或文本格式之一。

之前我们提到，`QDomDocument` 可以轻松写入文件。以下是我们如何做到的，假设 `dom` 是一个 `QDomDocument` 且 `filename` 是有效的文件名，但不包含错误检查：

```python
open(filename, "w", "utf-8").write(unicode(dom.toString()))
```

这将产生一个与 `exportXml()` 方法产生的文件略有不同的文件。例如，`QDomDocument.toString()` 方法会缩进嵌套标签，对属性使用双引号而不是单引号，并且可能会以不同的顺序排列属性。尽管如此，生成的 XML 文档在规范上与 `exportXml()` 生成的文档是相同的。

一旦 `QDomDocument` 读入了 XML 文件，我们需要遍历其内容来填充应用程序的数据结构，为此我们首先对文档调用 `populateFromDOM()`。

```python
def populateFromDOM(self, dom):
    root = dom.documentElement()
    if root.tagName() != "MOVIES":
        raise ValueError, "not a Movies XML file"
    self.clear(False)
    node = root.firstChild()
    while not node.isNull():
        if node.toElement().tagName() == "MOVIE":
            self.readMovieNode(node.toElement())
        node = node.nextSibling()
```

我们首先检查读取的 XML 文件是否确实是电影 XML 文件。如果否，我们会抛出异常；如果是，我们会清除数据结构，使其准备好接受从 DOM 文档提取的数据。
