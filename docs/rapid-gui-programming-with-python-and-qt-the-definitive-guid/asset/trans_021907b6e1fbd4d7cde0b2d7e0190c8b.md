
通常，我们会提供一种导入方法，并使用 SAX 或 DOM 解析器。在这里，我们选择同时展示两种解析器的使用，因此提供了两个独立的导入操作。两者产生的结果相同。

用于导入的文件操作代码与“文件打开”操作非常相似，只是我们使用了由用户指定的导入解析器。与所有文件处理代码一样，我们将工作委托给电影容器。

```python
def fileExportXml(self):
    fname = self.movies.filename()
    if fname.isEmpty():
        fname = "."
    else:
        i = fname.lastIndexOf(".")
        if i > 0:
            fname = fname.left(i)
        fname += ".xml"
    fname = QFileDIalog.getSaveFileName(self,
            "My Movies - Export Movie Data", fname,
            "My Movies XML files (*.xml)")
    if not fname.isEmpty():
        if not fname.contains("."):
            fname += ".xml"
        ok, msg = self.movies.exportXml(fname)
        self.statusbar().showMessage(msg, 5000)
```

我们只提供一种 XML 导出方法。代码类似于“文件另存为”操作。请注意，我们必须使用 QString 方法以确保文件名具有 .xml 扩展名，而不是我们在 Image Changer 应用程序中使用的 unicode 方法，因为文件名是以 QString 形式存储的。

## 数据容器职责

应用程序的数据容器负责持有所有数据项，即电影记录，并负责将它们保存和加载到磁盘。在前一节中，当我们查看 `MainWindow.updateTable()` 方法时，已经看到容器如何通过 for 循环进行迭代，以获取所有电影，从而在应用程序的 `QtWebKitWidget` 中显示它们。在本节中，我们将探讨 `moviedata` 模块提供的功能，包括用于存储电影数据的数据结构、如何提供支持有序迭代的功能以及其他方面，但排除实际的保存和加载代码，因为那将在后续章节中介绍。

为什么要使用自定义的数据容器？毕竟，我们可以简单地使用 Python 内置的数据结构，如列表或字典。我们倾向于采取一种方法，即将标准数据结构封装在自定义容器类中。这确保了数据的访问由我们的类控制，有助于维护数据完整性。它也使扩展容器功能并替换底层数据结构变得更加容易，且不会影响现有代码。换句话说，这是一种面向对象的方法，避免了简单地使用例如列表加全局函数的缺点。

我们将先从 `moviedata` 模块的导入和常量开始。

```python
import bisect
import codecs
import copy_reg
import cPickle
import gzip
from PyQt4.QtCore import *
from PyQt4.QtXml import *
```

我们将电影按规范化标题顺序存储，忽略大小写，并忽略开头的“A”、“An”和“The”字样。为了最小化插入和查找时间，我们使用 `bisect` 模块维护顺序，采用与我们在第 3 章中实现的 `OrderedDict` 相同的技术。

`codecs` 模块对于使用特定文本编码读写 Python 文本文件是必需的。`copy_reg` 和 `cPickle` 模块用于保存和加载 Python “pickles”——这些是包含任意 Python 数据结构文件。`gzip` 模块用于压缩数据；我们将用它来压缩和解压我们的 pickle 数据。`PyQt4`/`QtCore` 的导入很熟悉，但我们还必须导入 `PyQt4`/`QtXml` 模块以获取对 `PyQt` 的 SAX 和 DOM 解析器的访问权限。我们稍后将在各节中看到所有这些模块的使用情况。请注意，由于 `moviedata` 模块是一个纯数据处理模块，没有 GUI 功能，因此我们不需要 `PyQt4`/`QtGui` 模块。

```python
CODEC = "UTF-8"
NEWPARA = unichr(0x2029)
NEWLINE = unichr(0x2028)
```

我们希望使用 UTF-8 编解码器用于文本文件。这是一种 8 位 Unicode 编码，每个 ASCII 字符使用一个字节，其他字符使用两个或更多字节。它可能是文件中使用的最广泛的 Unicode 文本编码。通过使用 Unicode，我们可以存储当今几乎所有正在使用的人类语言文字的文本。

尽管 \n 是一个有效的 Unicode 字符，但在我们使用 XML 时，将需要使用特定的 Unicode 段落换行符和行换行符。这是因为 XML 解析器通常不区分不同的 ASCII 空白字符，例如换行符和空格，如果我们希望保留用户的行和段落换行，这是不方便的。

```python
class Movie(object):
    UNKNOWNYEAR = 1890
    UNKNOWNMINUTES = 0

    def __init__(self, title=None, year=UNKNOWNYEAR,
                 minutes=UNKNOWNMINUTES, acquired=None, notes=None):
        self.title = title
        self.year = year
        self.minutes = minutes
        self.acquired = acquired \
            if acquired is not None else QDate.currentDate()
        self.notes = notes
```

Movie 类用于保存关于一部电影的数据。我们直接使用实例变量，而不是提供简单的 getter 和 setter。标题和备注作为 QString 存储，获取日期作为 QDate。电影发布的年份和时长（以分钟计）作为 int 存储。我们提供两个静态常量来表示我们不知道电影何时发布或时长多久。

我们现在准备查看电影容器类。该类持有一个电影有序列表，并提供用于以多种格式保存和加载（以及导出和导入）电影的功能。

```python
class MovieContainer(object):
    MAGIC_NUMBER = 0x3051E
    FILE_VERSION = 100

    def _init(self):
        self.__fname = QString()
        self.__movies = []
        self.__movieFromId = {}
        self.__dirty = False
```

MAGIC_NUMBER 和 FILE_VERSION 用于使用 PyQt 的 QDataStream 类保存和加载文件。

文件名作为 QString 保存。`__movies` 列表中的每个元素本身是一个二元列表，第一个元素是排序键，第二个是 Movie。这是该类的主要数据结构，用于按顺序保存电影。`__movieFromId` 字典的键是 Movie 对象的 id()，值是 Movies。如我们在第 1 章所见，每个 Python 对象非常方便地拥有一个唯一 ID，可以通过调用其 id() 获得。此字典用于在已知电影 ID 时提供快速电影查找。例如，主窗口在 QTableWidgetItems 的第一列中存储电影 ID 作为“用户”数据。当然，没有数据重复，因为这两个数据结构实际上持有的是对 Movie 对象的引用，而不是 Movie 对象本身。

- id( ) 函数
- 对象引用

```python
def __iter__(self):
    for pair in iter(self.__movies):
        yield pair[1]
```

当 MainWindow.updateTable() 方法使用 for 循环迭代电影容器时，Python 使用了容器的 __iter__() 方法。在这里我们可以看到，我们迭代 [key, movie] 列表的有序列表，每次只返回 movie 项。

```python
def __len__(self):
    return len(self.__movies)
```

此方法允许我们对电影容器使用 len() 函数。

在后续章节中，我们将看到用于以各种格式加载和保存在电影容器中存储的电影的代码。但首先，我们将查看如何清除容器，以及如何添加、删除和更新电影，以便了解容器的运作方式，特别是关于顺序的部分。

```python
def clear(self, clearFilename=True):
    self.__movies = []
    self.__movieFromId = {}
    if clearFilename:
        self.__fname = QString()
    self.__dirty = False
```

此方法用于清除所有数据，可能包括文件名。它从 MainWindow.fileNew() 调用，该方法会清除文件名，也从各种保存和加载方法调用，这些方法不触及文件名。电影容器维护一个脏标志，以便始终知道是否有未保存的更改。

```python
def add(self, movie):
    if id(movie) in self.__movieFromId:
```
