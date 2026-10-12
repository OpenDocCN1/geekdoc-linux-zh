

super(MainForm, self).__init__(parent)
self.model = BarGraphModel()
self.barGraphView = BarGraphView()
self.barGraphView.setModel(self.model)
self.listView = QListView()
self.listView.setModel(self.model)
self.listView.setItemDelegate(BarGraphDelegate(0, 1000, self))
self.listView.setMaximumWidth(100)
self.listView.setEditTriggers(QListView.DoubleClicked |
QListView.EditKeyPressed)

layout = QHBoxLayOut()
layout.addWidget(self.listView)
layout.addWidget(self.barGraphView, 1)
self.setLayout(layout)

self.setWindowTitle("Bar Grapher")

在模型解决方案中，我们添加了一些额外的代码来创建 20 个随机项，以生成初始的条形图。整个过程可以在不到 200 行代码内完成。

解决方案位于 chap16/bargrapher.pyw。

*此页有意留白*

# 在线帮助与国际化工具

用户可能仅通过阅读菜单选项和按钮文本，就能使用非常简单的应用程序。其他应用程序可能需要更多的信息，在这种情况下，工具提示（tooltips）和状态提示（status tips）是一个易于编程的解决方案。但有些应用程序非常复杂或精妙，用户可能需要更广泛的帮助来理解有哪些可用功能，以及如何使用这些应用程序。

提供充分信息的解决方案之一是提供纸质手册；另一种是提供帮助系统。创建合适的在线帮助系统可以采用几种可能的途径；我们将提及所有这些途径，并展示其中一种。我们将回顾第 6 章介绍的图片更换器（Image Changer）应用程序，在本章的第一部分中，我们将展示该应用程序 MainWindow.helpHelp() 方法的实现，以及如何提供在线帮助系统。

在本书中，展示的应用程序提供的菜单文本、按钮文本、标签、提示等内容均为英文。对于世界上少数能阅读英语的人来说，这没问题，但对于说世界上最广泛使用的语言——普通话——的人来说，或对于说其他主要语言（如西班牙语、阿拉伯语、印地语、葡萄牙语、孟加拉语、俄语或日语）的人来说，这就没什么用了。

为了让应用程序尽可能被广泛使用，它必须对非英语使用者也易于访问。PyQt 提供了一套工具链，用于标识用户可见的字符串，并使这些字符串能够在易用的 Qt Linguist 图形界面应用程序中可用，人类翻译人员可以使用该应用程序提供适当的翻译。在本章的第二部分中，我们将讨论翻译工具并展示如何使用它们。我们还将展示一个经过改进的、支持翻译的图片更换器应用程序版本，以便与翻译工具配合使用。

![](img/9bfe0a027fcc8793bb087287001100dd_523_0.png)

# 在线帮助

提供在线帮助系统有三种常见方法。一种方法是提供 HTML 文件形式的帮助，并启动设置到相关页面的 Web 浏览器。另一种方法是使用随 Qt 提供的 *Qt Assistant* 应用程序。第三种方法是提供帮助表单，同样使用 HTML，但以图像和 HTML 文件作为资源。

![](img/9bfe0a027fcc8793bb087287001100dd_524_0.png)

*图 17.1 图片更换器帮助表单*

第一种方法可以通过启动一个独立的 Web 浏览器进程来实现，可以使用 Python 的 *subprocess* 模块，或者使用 PyQt 的 *QProcess* 类。Qt 4.2 引入了一个新类 *QDesktopServices*，通过其 *openUrl()* 静态便捷方法，以平台无关的方式启动浏览器变得非常简单。

第二种方法比较棘手，因为它要求我们创建一个特殊格式的 XML 文件，并随应用程序分发 *Qt Assistant*。使用 *Qt Assistant* 的优点是它提供自动索引功能。

第三种方法，使用自定义帮助表单，并以 HTML 文件和图像作为资源，是我们将要采用的方法。我们在第 6 章查看资源文件时看到，我们可以包含任意文件，包括 HTML 文件，我们将一些演示帮助文件集成到了 *resources.qrc* 文件中。以下是图片更换器的 *MainWindow.helpHelp()* 方法的代码：

def helpHelp(self):
    form = helpForm.HelpForm("index.html", self)
    form.show()

使用我们的帮助表单很简单：我们只需给它一个 HTML 文件和 self（表单将以此为中心）。注意，我们使用的是 show() 而不是 exec()；这几乎总是意味着显示的表单将设置“关闭时删除”属性。

图 17.1 中的截图可能会让人产生键盘用户未被照顾到的错误印象，但事实上，用于显示 HTML 文件的类 QTextBrowser 提供了良好的键盘支持。例如，用户可以按 Tab 键在超链接之间移动焦点，按 Enter 键跟随超链接。他们可以按 Alt+左箭头键返回，按 Home 键前往第一页。并且，由于表单是 QDialog 的子类，他们可以通过按 Esc 键关闭窗口。

此时我们非常熟悉创建 PyQt 对话框，因此我们仅展示与创建在线帮助系统相关的摘录——具体来说，HelpForm 初始化程序中的几段摘录，以及它的一个方法。（代码位于 chap17/helpform.py。）

class HelpForm(QDialog):

    def __init__(self, page, parent=None):
        super(HelpForm, self).__init__(parent)
        self.setAttribute(Qt.WA_DeleteOnClose)
        self.setAttribute(Qt.WA_GroupLeader)

Qt.WA_GroupLeader 属性确保如果帮助表单从模态对话框调用，用户能够同时与模态对话框和帮助表单交互，否则这是不可能的。如果帮助表单从无模态对话框或主窗口调用，该属性没有效果，用户可以照常与两者交互。

self.textBrowser.setSearchPaths([":/"])
self.textBrowser.setSource(QUrl())

QTextBrowser 类是 QTextEdit 的子类，可用于显示大量 HTML 标签的子集，包括图像、列表和表格。我们将搜索路径设置为资源文件的根目录，并设置初始页面为传入的页面。因为我们设置了搜索路径，所以可以传入没有路径的页面（例如，仅仅是 index.html 或 filemenu.html）。QTextBrowser 理解资源路径，因此能够在如 `<img src=":/filenew.png">` 这样的 `<img>` 标签中找到图像资源。

self.connect(backAction, SIGNAL("triggered()"),
            self.textBrowser, SLOT("backward()"))
self.connect(homeAction, SIGNAL("triggered()"),
            self.textBrowser, SLOT("home()"))
self.connect(self.textBrowser, SIGNAL("sourceChanged(Qurl)"),
            self.updatePageTitle)

页面之间的导航由 QTextBrowser 自动处理。尽管如此，我们提供了两个工具栏按钮，“返回”和“主页”，并将它们连接到适当的 QTextBrowser 槽，以获得我们想要的行为。如果 HTML 文档发生变化——例如，由于用户点击了超链接——我们调用自定义的 updatePageTite() 槽。

def updatePageTite(self): self.pageLabel.setText(self.textBrowser.documentTite())

该槽只是将 HTML 页面的 _title> 文本放在工具栏中的 QLabel 中，位于工具栏按钮的右侧。

一旦我们有了 HelpForm 类，就可以完全使用 HTML 来实现我们的在线帮助系统，要么将文件包含为资源，要么将它们安装到文件系统中，并使用如下代码查找它们：

helppath = os.path.join(os.path.dirname(_ file_), "help")

这假设帮助文件位于应用程序 .py 文件所在目录下的 help 目录中。

编写提供在线帮助系统的代码很直接；但设计一个易于导航且易于理解的系统可能相当具有挑战性。

# # 国际化工具

使应用程序适合说与原始语言不同的语言的用户时，需要考虑几个问题。最大且最明显的问题是，所有用户可见的字符串必须翻译成目标语言，这不仅包括用于菜单选项和对话框按钮的字符串，还包括工具提示、状态提示和其他任何在线帮助。此外，我们还必须执行其他本地化操作，例如确保数字使用适当的小数标记和千位分隔符，时间和日期格式正确，纸张尺寸和计量系统正确。例如，大多数美国人和英国人说英语，但这两种文化有不同的日期格式约定、不同的货币、不同的标准纸张尺寸和不同的计量系统。

得益于 Unicode 的使用，几乎所有人类语言使用的任何字符都可以显示。我们在书的开头附近看到，可以使用 unicode 转义字符和目标字符的十六进制代码点，或者使用 unichr() 函数，在 unicode 或 QString 字符串中包含任何 unicode 字符。至于读取和写入包含 Unicode 的文本文件，我们可以使用 Python 的 codecs.open() 函数，或者如我们在前面章节中看到的，使用 PyQt 的 QTextStream。

