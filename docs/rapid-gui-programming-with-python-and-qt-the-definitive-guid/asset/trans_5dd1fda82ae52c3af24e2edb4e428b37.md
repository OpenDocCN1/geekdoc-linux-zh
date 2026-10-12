

我们获取一个 QFile 文件句柄，并将其转换为 XML “输入源”。此时我们再次尽可能晚地清空我们的数据结构，然后告诉解析器解析该 XML 文件。解析器在成功时返回 True，在失败时返回 False。

由于我们在解析过程中通过我们的 SaxMovieHandler 类内部处理所有这些，因此没有专门用于填充数据结构的阶段。最后，我们清空文件名并将脏标记设置为 True，就像我们在 importDOM() 方法结束时所做的那样。

SaxMovieHandler 类是 QXmlDefaultHandler 的子类。对于内容处理，通常至少需要实现 startElement()、endElement() 和 characters()，以处理带有属性的开始标签、结束标签以及标签之间的文本。如果我们像这里一样使用同一个处理器来处理错误，我们还必须至少实现 fatalError() 方法。

```python
class SaxMovieHandler(QXmlDefaultHandler):
  def __init__(self, movies):
    super(SaxMovieHandler, self).__init__()
    self.movies = movies
    self.text = QString()
    self.error = None
```

super() 调用确保基类被正确初始化。movies 参数是电影容器本身。text 实例变量用于保存标签之间的文本——例如标题或备注文本——如果出现问题，error 变量将被赋予错误消息。

```python
def clear(self):
  self.year = None
  self.minutes = None
  self.acquired = None
  self.title = None
  self.notes = None
```

第一次调用此方法时，它会为电影的每个属性创建一个实例变量。每次调用时它都会将变量设置为 None；这将使测试我们是否已读取电影的所有属性变得容易。

```python
def startElement(self, namespaceURI, localName, qName, attributes):
  if qName == "MOVIE":
    self.clear()
    self.year = intFromQStr(attributes.value("YEAR"))
    self.minutes = intFromQStr(attributes.value("MINUTES"))
    ymd = attributes.value("ACQUIRED").split("-")
    if ymd.count() != 3:
      raise ValueError, “invalid acquired date %s” % \
          unicode(attributes.value("ACQUIRED"))
    self.acquired = QDate(intFromQStr(ymd[0]),
intFromQStr(ymd[1]),
        intFromQStr(ymd[2]))
    elif qName in ("TITLE", "NOTES"):
        self.text = QString()
    return True
```

此方法是从基类重新实现的，因此我们必须使用相同的签名。我们只对最后两个参数感兴趣：qName（限定名），它保存标签名称，以及 attributes，它保存标签的属性数据。每当遇到新的开始标签时，都会调用此方法。

如果遇到新的 <MOVIE> 标签，我们清空相应的实例变量，然后从标签属性数据中填充年份、分钟数和获取日期。这将使 title 和 notes 变量保持为 None。

如果标签是 <TITLE> 或 <NOTES> 标签，我们可以预期获得其对应的文本（如果有），因此我们将 text 变量设置为空字符串，以便随时追加内容。

每个重新实现的方法在成功时必须返回 True，在失败时返回 False；因此我们在最后返回 True。

```python
def characters(self, text):
    self.text += text
    return True
```

每当在标签之间遇到文本时，都会调用 characters() 方法。我们只需将文本追加到 text 变量。结束标签会告诉我们我们是在累积标题还是备注文本。

```python
def endElement(self, namespaceURI, localName, qName):
    if qName == "MOVIE":
        if self.year is None or self.minutes is None or \
            self.acquired is None or self.title is None or \
            self.notes is None or self.title.isEmpty():
            raise ValueError, "incomplete movie record"
        self.movies.add(Movie(self.title, self.year,
            self.minutes, self.acquired,
            decodedNewlines(self.notes)))
        self.clear()
    elif qName == "TITLE":
        self.title = self.text.text.trimmed()
    elif qName == "NOTES":
        self.notes = self.text.text.trimmed()
    return True
```

此方法在遇到结束标签时调用。标签名称在 qName 参数中。如果结束标签是 </MOVIE>，电影数据实例变量均不应为 None（尽管 title 或 notes 可以是空的 QString）。

如果所有变量都不是 `None`，并且电影有标题，我们就创建一个新的 `Movie` 对象并立即将其添加到 movies 容器中。

如果我们到达了标题或备注的结束标签，我们就知道累积在 text `QString` 中的文本是对应开始标签和结束标签之间的文本，因此我们相应地分配该文本。如果没有文本，赋值将是空的 `QString`。

```python
def fatalError(self, exception):
    self.error = "parse error at line %d column %d: %s" % (
        exception.lineNumber(), exception.columnNumber(),
        exception.message())
    return False
```

如果发生解析错误，将调用 `fatalError()` 方法。我们重新实现它，以填充处理程序的 `error` 文本，并返回 `False` 表示失败。这将导致解析器结束解析并向其调用者返回 `False`。

使用 PyQt 的 SAX 解析器要求我们至少创建一个独立的手动处理子程序。这并不困难，特别是我们只需要重新实现我们想要使用的方法。使用 SAX 进行解析比使用 DOM 消耗更少的内存，因为 SAX 是增量工作的，并且明显更快，特别是对于较大的文档。

## 摘要

在所有可用的选择中，哪种格式最适合使用，我们应该使用 Python 还是 PyQt 类？

对于性能和平台独立性，使用二进制格式是最好的，也是实现最简单的。对于通常只包含简单值（如字符串、数字和日期）且旨在手动编辑的小型文件，使用纯文本格式是合适的。即便如此，仍然存在用户的文本编辑器假设的编码与我们使用的编码不同的风险。我们建议对所有纯文本格式使用 UTF-8，因为它正在成为事实上的标准编码。读写 XML 比读写二进制文件慢得多（对于小于 ~1MB 的小文件除外），但至少作为导出和导入格式提供是值得的。毕竟，如果我们的用户能够以 XML 格式导出和导入数据，这就赋予了他们导出数据、使用其他工具处理它，然后导回处理后的数据的能力，而无需了解或关心我们的应用程序通常使用的二进制格式的详细信息。

至于是否使用 Python 或 PyQt 类，对于包含简单数据类型的较小文件，这可能完全无关紧要。如果我们想将编程工作量最小化，使用 `cpickle` 模块可能是最简单的途径。但是，如果我们有大文件（数兆字节）或者使用复杂的 PyQt 类型，如 `QBrush`、`QCursor`、`QFont`、`QIcon`、`QImage` 等，使用 `QData5tream` 是最简单和最高效的，因为它可以直接读写所有这些类型。使用二进制格式的一个缺点是，如果我们想更改格式，我们至少必须更改我们的 load 方法，使其能够加载新格式和旧格式。这在实践中不是问题，只要我们在魔术数字后的数据开头包含文件版本，因为我们可以使用它来确定使用哪种加载代码。

在这个阶段，我们已经涵盖了 GUI 编程的基础知识。我们可以创建带有菜单、工具栏和停靠窗口的主窗口应用程序，并且可以创建和弹出任何我们喜欢的对话框。我们还学习了如何使用 Qt Designer 简化和加快对话框设计，并看到了如何以各种格式加载和保存应用程序数据。在第三部分中，我们将深化和拓宽我们的 GUI 编程知识，学习如何处理多个文档以及创建对用户可以管理的复杂对话框。我们还将探索 PyQt 的一些主要架构功能，从其低级事件处理机制到创建自定义小部件，包括 2D 图形的覆盖，以及更高级的功能，包括基于项目的图形、富文本（HTML）处理以及模型/视图编程。

## 练习

修改 My Movies 应用程序，使每个 Movie 对象可以存储额外的信息：一个名为 “location” 的 QString，表示电影的所在位置——例如房间和书架。仅提供保存和加载二进制 Qt 格式的 .mpb 文件以及导出和导入 XML 文件，因此删除用于保存和加载 pickle 和文本文件的代码。确保你的新 My Movies 应用程序仍然可以读取原始应用程序的 .mpb 和 .xml 文件，即没有 location 数据的文件。

moviedata 模块中的 Movie 类需要一个额外的 QString 属性，称为 “location”。MovieContainer 类需要进行几处小改动。你需要同时拥有旧版本和当前版本的文件版本号，以便知道你在处理哪种类型。formats() 方法现在应该只返回字符串 “.mpb”，或者可以完全取消。save() 和 load() 方法只需要处理 .mpb 文件，并且必须考虑 location 和不同的文件版本。同样，exportXml() 方法和两个 import XML 方法也必须考虑可能存在 <LOCATION> 标签。用户界面的更改应该是显而易见的，所以我们不会列出它们。

这些更改中的任何一个都不涉及很多代码行，但有些是细微的，需要一点小心才能做对。确保你测试了你的更改。例如，加载旧格式的 .mpb 文件，并导入旧 .xml 格式的文件。添加一些位置并将数据保存到新的 .mpb 文件并导出为 XML。读回这两个以检查一切是否正常工作。

模型解决方案提供在以下文件中：chap08/mymovies_ans.pyn, chap08/moviedata_ans.pyn, chap08/addeditmowidlg_ans.ui, 和 chap08/addeditmowidlg_ans.py。

