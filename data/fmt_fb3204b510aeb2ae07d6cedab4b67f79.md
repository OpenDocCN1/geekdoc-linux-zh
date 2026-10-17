
DOM 文档由“节点”组成，每个节点代表一个 XML 标签或标签之间的文本。一个节点可以有子节点，也可以有兄弟节点。在电影 XML 格式中，我们有作为兄弟节点的 `<MOVIE>` 节点，它们拥有 `<TITLE>` 和 `<NOTES>` 子节点，而这些子节点又有子文本节点。因此，为了提取数据，我们遍历 `<MOVIE>` 节点，对于遇到的每一个，我们提取其属性及其子节点中的数据。

```python
def readMovieNode(self, element):
    def getText(node):
        child = node.firstChild()
        text = QString()
        while not child.isNull():
            if child.nodeType() == QDomNode.TextNode:
                text += child.toText().data()
            child = child.nextSibling()
        return text.trimmed()
```

`readMovieNode()` 以一个嵌套函数定义开始。`getText()` 函数以一个节点作为参数——例如，`<TITLE>` 或 `<NOTES>` 开始标签——并遍历其子文本节点，累积它们的文本。最后，它返回文本，去除两端空白。如前所述，`QString.trimmed()` 方法执行与 `unicode.strip()` 相同的工作。

```python
year   = intFromQStr(element.attribute("YEAR"))
minutes = intFromQStr(element.attribute("MINUTES"))
ymd = element.attribute("ACQUIRED").split("-")
if ymd.count() != 3:
    raise ValueError, "invalid acquired date %s" % \
        unicode(element.attribute("ACQUIRED"))
acquired = QDate(intFromQStr(ymd[0]), intFromQStr(ymd[1]),
                 intFromQStr(ymd[2]))
```

`readMovieNode()` 方法本身通过提取 `<MOVIE>` 标签的属性数据并将从文本转换为年数和分钟数的整数，以及将获取日期转换为 `QDate` 而开始。

我们可以避免自行处理获取日期的细节，并将工作推给解析器。例如，而不是只有一个 `ACQUIRED` 属性，我们可以有 `ACQUIREDYEAR`、`ACQUIREDMONTH` 和 `ACQUIREDAY`，每个都有一个整数值。使用这三个属性，我们就不需要对连字符进行拆分，但格式会更加冗长。

```python
title = notes = None
node = element.firstChild()
while title is None or notes is None:
    if node.isNull():
        raise ValueError, "missing title or notes"
    if node.toElement().tagName() == "TITLE":
        title = getText(node)
    elif node.toElement().tagName() == "NOTES":
        notes = getText(node)
    node = node.nextSibling()
    if title.isEmpty():
        raise ValueError, "missing title"
self.add(Movie(title, year, minutes, acquired,
               decodedNewlines(notes)))
```

每个 `<MOVIE>` 节点有两个子节点，`<TITLE>` 和 `<NOTES>`。尽管我们在 `exportXml()` 方法中始终以相同的顺序写入它们，但我们不希望强制子节点具有特定的顺序。为此，我们遍历子节点，并使用嵌套的 `getText()` 方法收集所遇到的子节点的文本。

最后，只要电影有标题，我们就创建一个新的 `Movie` 对象，并立即使用 `add()` 将其添加到我们的数据结构中。

使用 DOM 解析器将 XML 导入自定义数据结构运行良好，尽管我们经常需要编写像 `getText()` 这样的小型辅助函数。DOM 最适合用于我们希望在 `QDomDocument` 本身内部持有和操纵 XML 数据，而不是将其转换为其他数据结构的情况。

### 使用 PyQt 的 SAX 类读取和解析 XML

使用 SAX 解析器导入 XML 与使用 DOM 解析器的工作方式有很大不同。在 SAX 中，我们定义一个处理器类，该类仅实现我们感兴趣的方法，然后将处理器的实例提供给 SAX 解析器，在解析 XML 时使用。解析不是像 DOM 那样一次性完成的，而是逐段进行的，当遇到其处理的数据时，调用我们处理器中的方法。任何我们未实现的方法都由基类提供，并且在所有情况下，它们都安全地不做任何事。

```python
def importSAX(self, fname):
    error = None
    fh = None
    try:
        handler = SaxMovieHandler(self)
        parser = QXmlSimpleReader()
        parser.setContentHandler(handler)
        parser.setErrorHandler(handler)
        fh = QFile(fname)
        input = QXmlInputSource(fh)
        self.clear(False)
        if not parser.parse(input):
            raise ValueError, handler.error
    except (IOError, OSError, ValueError), e:
        error = "Failed to import: %s" % e
    finally:
        if fh is not None:
            fh.close()
        if error is not None:
            return False, error
        self.__name = QString()
        self.__dirty = True
        return True, "Imported %d movie records from %s" % (
            len(self.__movies), QFileInfo(fname).fileName())
```

我们首先创建一个自定义 `SaxMovieHandler` 和 SAX XML 解析器的实例。解析器可以接受内容处理器、错误处理器，或者同时接受两者；我们选择只创建一个处理器，该处理器可以同时处理内容和错误，因此我们将同一个处理器用于这两个目的。

我们获取一个 `QFile` 文件句柄，并将其转换为 XML “输入源”。此时我们再次尽可能晚地清空我们的数据结构，然后告诉解析器解析该 XML 文件。解析器在成功时返回 `True`，在失败时返回 `False`。

由于我们在解析过程中通过我们的 `SaxMovieHandler` 类内部处理所有这些，因此没有专门用于填充数据结构的阶段。最后，我们清空文件名并将脏标记设置为 `True`，就像我们在 `importDOM()` 方法结束时所做的那样。

`SaxMovieHandler` 类是 `QXmlDefaultHandler` 的子类。对于内容处理，通常至少需要实现 `startElement()`、`endElement()` 和 `characters()`，以处理带有属性的开始标签、结束标签以及标签之间的文本。如果我们像这里一样使用同一个处理器来处理错误，我们还必须至少实现 `fatalError()` 方法。

```python
class SaxMovieHandler(QXmlDefaultHandler):
  def __init__(self, movies):
    super(SaxMovieHandler, self).__init__()
    self.movies = movies
    self.text = QString()
    self.error = None
```

`super()` 调用确保基类被正确初始化。`movies` 参数是电影容器本身。`text` 实例变量用于保存标签之间的文本——例如标题或备注文本——如果出现问题，`error` 变量将被赋予错误消息。
