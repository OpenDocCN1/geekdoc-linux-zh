

## 国际化

在处理本地化的某些方面时，我们可以使用 QString、QDate 和 QTime。例如，假设 n 是一个数字，`QString("%1").arg(n)` 将生成一个带有适合当前区域设置的千位分隔符和小数点分隔符的 QString。QDate 和 QTime 都具有 `toString()` 方法，该方法可以接受自定义格式，或者预定义格式，例如 `Qt_SystemLocaleDate`（在旧代码中为 `Qt_LocalDate`），或者“通用”的 `Qt_1500Date`。此外，QLocale 类提供了许多用于返回本地化 QString 的方法，以及一些用于从本地化 QString 中提取数字的方法。它还具有返回特定区域设置字符的方法，例如用作负号、百分比符号等的字符。

国际化应用程序的大部分工作都涉及翻译，因此本节剩余部分将重点讨论这一主题。

为了帮助翻译应用程序，PyQt 提供了一组由三个工具组成的工具链：pyuic4、lrelease 和 Qt Linguist。为了使这些工具有用，所有用户可见的字符串都必须进行特殊标记。这可以通过使用 QObject.tr() 方法轻松实现，该方法被所有 QWidget 子类继承，包括所有对话框和主窗口。例如，我们不再编写 `QString("&Save")`，而是编写 `self.tr("&Save")`。传递给 tr() 的文本应该是 ASCII 字符；如果需要超出 ASCII 范围的字符，请改用 `trUtf8()`。

对于标记为需翻译的字符串，翻译工具会获得一对字符串：一个“上下文”字符串（类名）和标记的字符串本身。上下文的目的是帮助人类翻译者识别该待翻译字符串显示在哪个窗口中，因为在某些语言中，不同窗口可能需要不同的翻译。

对于需要翻译但不在类内部的字符串，我们必须使用 QApplication.translate() 方法，并自己提供上下文字符串。例如，在 main() 函数中，我们可以这样翻译应用程序名称：`QApplication.translate("main", "Gradgrind")`。在这里，上下文是 "main"，待翻译的字符串是 "Gradgrind"。

不幸的是，self.tr() 使用的上下文可能与 C++/Qt 的 tr() 方法使用的上下文不同，因为 PyQt 动态确定上下文，而 C++ 在编译时确定上下文。如果翻译文件在 C++/Qt 和 PyQt 应用程序之间共享，这可能很重要。如果表单是子类，这也可能是一个问题。如果这确实成为一个问题，解决方案很简单：将每个单参数的 self.tr() 调用替换为双参数的 QApplication.translate() 调用，明确将正确的上下文作为第一个参数，将待翻译字符串作为第二个参数。

一旦应用程序的所有用户可见字符串都合适地标记完毕，我们就必须稍微修改应用程序的启动方式，以便读取其运行所在区域设置的翻译字符串。

> *请参阅 PyQt 的 pyqt4ref.html 文档，位于“PyQt 与 Qt 之间的差异”部分下。

以下是创建国际化应用程序的方法：

- 使用 QObject.tr() 或 QApplication.translate() 创建应用程序，用于所有用户可见的字符串。
- 修改应用程序，以便在启动时如果可用，读取特定于区域设置的 .qm（Qt 消息）文件。
- 创建一个 .pro 文件，列出应用程序的 .ui（Qt Designer）文件、.py 和 .pyw 源文件，以及它将使用的 .ts（翻译源）文件。
- 运行 pyuic4 以创建 .ts 文件。
- 要求翻译者使用 Qt Linguist 翻译 .ts 文件中的字符串。
- 运行 lrelease 将更新后的 .ts 文件（包含翻译）转换为 .qm 文件。

以下是维护此类应用程序的方法：

- 更新应用程序，确保所有用户可见的字符串使用 QObject.tr() 或 QApplication.translate()。
- 如有必要，更新 .pro 文件——例如，添加已添加到应用程序的任何新 .ui 或 .py 文件。
- 运行 pyuic4 以使用任何新字符串更新 .ts 文件。
- 要求翻译者翻译 .ts 文件中的任何新字符串。
- 运行 lrelease 将 .ts 文件转换为 .qm 文件。

我们将涵盖上述所有步骤，从使用 QObject.tr() 开始，使用 chap17 目录中翻译感知版 Image Changer 应用程序的摘录。

```python
fileNewAction = self.createAction(self.tr("SNew..."),
    self.fileNew, QKeySequence.New, "filenew",
    self.tr("Create an image file"))
```

第一个标记为待翻译的字符串是菜单选项字符串，New...，第二个是用于工具提示和状态提示的字符串。（"filenew" 字符串是图标文件的名称，不包括其 .png 后缀。）

```python
self.fileMenu = self.menuBar().addMenu(self.tr("&File"))
```

菜单字符串以及操作字符串都必须进行翻译。

```python
self.statusBar().showMessage(self.tr("Ready"), 5000)
```

这里有一个初始状态消息给用户，我们再次必须使用 tr()。

通常，翻译用作 QSettings 键的字符串并不合适，特别是因为这些字符串通常对用户不可见。

```python
reply = QMessageBox.question(self,
    self.tr("Image Changer - Unsaved Changes"),
    self.tr("Save unsaved changes?"),
    QMessageBox.Yes | QMessageBox.No | QMessageBox.Cancel)
```

对于此消息框，我们已标记窗口标题和消息文本以进行翻译。在这种情况下，我们不必担心翻译按钮，因为我们使用的是标准按钮，且 Qt 已提供这些按钮的翻译。如果我们使用自定义文本，就必须像其他任何用户可见字符串一样对它使用 tr()。

```python
self.tr("Saved %1 in file %2").arg(self.dataname).arg(self.filename)
```

提供上述字符串的一种方式是编写：

```python
self.tr("Saved %s in file %s" % (self.dataname, self.filename)) # BAD
```

不推荐这样做。始终使用 QString，并始终使用 QString.arg()；这使翻译工作更容易。（tr() 方法返回一个 QString，因此我们可以对其返回值调用任何 QString 方法，如 arg()。）例如，在某些语言中，翻译可能被表述为“数据 %1 保存在文件 %2 中”。使用带有 arg() 的 QString 并非问题，因为翻译者可以更改字符串中 %s 的顺序，且 arg() 方法将尊重此顺序。但在 Python 字符串中互换一个 %s 为另一个并不会改变任何东西。

在手写的 .py 和 .pyw 文件中，我们必须对每个用户可见的字符串使用 tr()。但对于由 pyuic4 从 .ui 文件生成的 .py 文件，我们无需做任何事，因为 pyuic4 无论如何都会自动对所有字符串使用 QApplication.translate()。即使对于未翻译的应用程序，这也有效，因为如果没有合适的翻译，将使用原始语言——例如英语。

PyQt 应用程序通常使用 PyQt 内置对话框；例如，文件打开对话框或文件打印对话框。这些也必须进行翻译，尽管对于几种语言，Trolltech 提供的 .qm 文件中已包含翻译。

既然我们在整个过程中使用了 tr()，并找到了合适的 Qt 翻译，我们就准备好修改应用程序的启动代码，以便在存在合适的翻译文件时加载它们。

```python
app = QApplication(sys.argv)
locale = QLocale.system().name()
qtTranslator = QTranslator()
if qtTranslator.load("qt_" + locale, ":/"):
    app.installTranslator(qtTranslator)
```

> *Trolltech 为某些语言（如法语和德语）以及一些其他不受支持的语言提供翻译。这些翻译位于 Qt（而非 PyQt）的翻译目录中；例如，在文件系统中搜索 qt_fr.qm 即可找到法语翻译。

```python
appTranslator = QTranslator()
if appTranslator.load("imagechanger_" + locale, ":"):
    app.installTranslator(appTranslator)

app.setOrganizationName("QTrac Ltd.")
app.setOrganizationDomain("qtrac.eu")
app.setApplicationName(app.translate("main", "Image Changer"))
app.setWindowIcon(QIcon(":/icon.png"))
form = MainWindow()
form.show()
app.exec_()
```

QLocale.system().name() 调用将返回诸如 “en_US”（英语，美国）或 “fr_CA”（法语，加拿大）等字符串。QTranslator.load() 方法接受文件主体和路径。在这种情况下，我们给定了路径 :/，它是应用程序的资源文件。如果区域设置为 “fr_CA”，文件主体将是 qt_fr_CA 和 imagechanger_fr_CA。基于此，PyQt 将查找 qt_fr_CA.qm，如果失败，则查找 qt_fr_CA，同样地查找 imagechanger_fr_CA.qm，如果失败，则查找 imagechanger_fr.qm。如果区域设置为 “en_US”，将找不到对应的 .qm 文件，因此不会安装任何翻译器——这是正常的，因为应用程序随后将回退使用原始字符串，而这些字符串本来就是英语。

请注意，我们必须使用 QApplication.translate()（写作 app.translate()），因为这段代码不在 QObject 子类的方法内。由于没有类名，我们选择使用文本 “main” 作为上下文；一些程序员可能更喜欢使用 “global”。我们可以自由选择任何喜欢的名称——上下文的目的纯粹是帮助人类翻译者。

我们只能将单一翻译加载到单个 QTranslator 对象中，但我们可以向 QTranslator 对象添加任意数量的翻译器。如果存在冲突，即同一字符串有不同的翻译，最近安装的翻译器将获胜。

尽管我们选择将翻译包含在资源文件中，但并没有这样做的义务；我们也可以同样容易地从文件系统访问它们。

以下是我们使用的 resource.qrc 文件中的摘录：

```xml
<qresource>
<file>qt_fr.qm</file>
<file>imagechanger_fr.qm</file>
</qresource>
<qresource>
<file alias="editmenu.html">help/editmenu.html</file>
<file alias="filemenu.html">help/filemenu.html</file>
<file alias="index.html">help/index.html</file>
</qresource>
<qresource lang="fr">
```

