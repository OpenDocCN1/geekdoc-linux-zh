
```cpp
void HelpBrowser::showPage(const QString &page)
{
    QString path = directoryOf("doc").absolutePath();
    HelpBrowser *browser = new HelpBrowser(path, page);
    browser->resize(500, 400);
    browser->show();
}
```

在`showPage()`静态函数中，我们创建了`HelpBrowser`窗口并显示它。当用户关闭它时，它会被销毁，因为我们在`HelpBrowser`构造函数中设置了`Qt::WA_DeleteClose`属性。在本示例中，假设文档位于应用程序目录。传递给`showPage()`函数的所有页面将从该子目录获取。

现在我们准备好从应用程序中调用帮助浏览器了。在应用程序的主窗口中，我们创建了一个帮助动作，并将其连接到`help()`槽，该槽可能如下所示：

```cpp
void MainWindow::help()
{
    HelpBrowser::showPage("index.html");
}
```

这假设主文件名为`index.html`。对于对话框，我们将帮助按钮连接到`help()`槽，该槽可能如下所示：

```cpp
void EntryDialog::help()
{
    HelpBrowser::showPage("forms.html#editing");
}
```

# 17. 提供帮助

在这里我们查看另一个帮助文件`forms.html`，并将`QTextBrowser`滚动到`editing`锚点。

也可以使用 Qt 的资源系统将帮助文件和相关图像直接嵌入到可执行文件中。实现此目标所需的唯一更改是为每个想要嵌入的文件在应用程序的`.qrc`文件中添加条目，并使用资源路径（例如`:/doc/forms.html`）。

在本示例中，我们同时使用了两种方法：嵌入图标（因为应用程序也使用了它们），但将我们的 HTML 文件保留在文件系统中。这样做的处是帮助文件可以独立于应用程序进行更新。

## 使用 Qt Assistant 获得强大的帮助

Qt Assistant 是由 Trolltech 提供的可重新分发的帮助应用程序。它的主要优点是支持索引和全文搜索，并且它可以处理多个应用程序的文档。要使用 Qt Assistant，我们必须在应用程序中包含必要的代码，并且必须让 Qt Assistant 感知到我们的文档。

Qt 应用程序与 Qt Assistant 之间的通信由`QAssistantClient`类处理，该类位于单独的库中。将此库链接到应用程序，我们必须在应用程序的`.pro`文件中添加此行：

```pro
CONFIG += assistant
```

我们现在将审查使用 Qt Assistant 的新`HelpBrowser`类代码。

```cpp
class HelpBrowser {
public:
    static void showPage(const QString &page);
private:
    static QString directoryOf(const QString &subdir);
    static QAssistantClient *assistant;
};
```

这里是新的`showPage()`实现：

```cpp
void HelpBrowser::showPage(const QString &page) {
    QString path = directoryOf("doc").absoluteFilePath(page);
    if (!assistant)
        assistant = new QAssistantClient("");
    assistant->showPage(path);
}
```

Qt 4.4 具有一个重构的帮助系统，这将使得集成我们的文档更加容易。`QAssistantClient`构造函数接受路径字符串作为第一个参数，它用它来定位 Qt Assistant 可执行文件。通过传递空路径，我们表示`QAssistantClient`在`PATH`变量中查找可执行文件。`QAssistantClient`有一个`showPage()`函数，接受带可选 HTML 锚点的页面名。

下一步是为文档准备目录和索引。这是通过创建一个 Qt Assistant 配置文件并编写一个提供文档信息的`.q`文件来完成的。所有这些内容在 Qt Assistant 的在线文档中都已解释，因此我们在这里不再重复。

使用 Web 浏览器、`QTextBrowser` 或 Qt Assistant 的替代方案是使用平台特定的方法提供在线帮助。对于 Windows 应用程序，创建 Windows 帮助文件并使用 Microsoft Internet Explorer 访问它们可能是理想的。你可以使用 Qt 的`QProcess`类或 ActiveQt 框架来实现此。在 OS X 上，Apple Help 提供了与 Qt Assistant 类似的功能。

我们现在到达了第二部分的结束。第三部分接下来的章节将涵盖 Qt 更高级、更专门的功能。这里呈现的 C++ 和 Qt 代码并不比我们在第二部分中展示的代码困难，但对于你来说是新领域，其中的某些概念和想法可能更具挑战性。

# 第三部分

# 高级 Qt

![](img/93c1c6fda99d42)

- 使用 Unicode

- 制作应用程序的感知

- 语言切换

- 翻译应用程序

# 18. 国际化

除了用于英语的语言外，Qt 还支持许多语言的输入方法。Unicode 的原始想法是，通过使用 16 位存储字符而不是 8 位，可以编码 65000 个字符。Unicode 包含了 ASCII 和 ISO 8859-1（Latin-1）作为子集。例如，字符 'A' 在 ASCII、Latin-1 和 Unicode 中的值都是`0x41`。

`QString`类以 Unicode 存储字符串。`QString`中的每个字符都是 16 位`QChar`。以下是将字符串第一个字符设置为 'A' 的两种方法：

```cpp
str[0] = 'A';
str[0] = QChar(0x41);
```

如果源文件以 Latin-1 编码，指定 Latin-1 字符只需：

```cpp
str[0] = '\N';
```

如果源文件有其他编码，数值值也可以正常工作：

```cpp
str[0] = QChar(0xD1);
```

对于某些语言需要特殊的输入方法，但 Qt 对于`QLineEdit`和`QTextEdit`控件来说运行良好。

- 许多应用程序需要根据本地设置进行翻译，整个界面也必须翻译。使用`tr()`函数包装所有可见字符串。

- 许多应用程序在启动时加载翻译文件，根据用户的区域设置。

- 在极少数情况下，用户可以在运行时切换语言。这对于 Qt 来说是完全可能的，尽管需要一些额外工作。

- 得益于 Qt 的布局系统，各种用户界面会自动调整。

## 使用 Unicode

elems。假设已经安装了正确的输入法，用户将能够在 Qt 应用程序中输入这些文字系统。

使用`QChar`编程与使用`char`编程略有不同。要获取`QChar`的数值值，请调用`unicode()`。要获取`QChar`的 ASCII 或 Latin-1 值（作为`char`），请调用`toLatin1()`。对于非 Latin-1 字符，`toLatin1()`将返回`\0`。

如果我们知道程序中的所有字符串都是 ASCII，我们可以在`toLatin1()`的返回值上使用`<cctype>`中的函数，如`isalpha()`、`isdigit()`和`isspace()`。然而，使用`QChar`的成员函数来执行这些操作会更好，因为它们适用于任何 Unicode 字符。`QChar`提供的函数有`isPrint()`、`isPunct()`、`isSpace()`、`isMark()`、`isLetter()`、`isNumber()`、`isLetterNumber()`、`isDigit()`、`isSymbol()`、`isLower()`和`isUpper()`。例如，这里是测试一个字符是否为数字或大写字母的一种方法：

```cpp
if (ch.isDigit() || ch.isUpper())
```

该代码段适用于任何区分大写和小写的的字母表，包括拉丁字母、希腊字母和西字母（Cyclic）。

一旦我们有了 Unicode 字符串，我们可以在任何期望`QString`的 Qt API 地方使用它。然后由 Qt 负责正确显示它，并在与操作系统通信时将其转换为各种编码。

在读写文本文件时需要特别注意。文本文件可以使用多种编码，通常无法根据其内容推断文本文件的编码。默认情况下，`QTextStream`使用系统本地的 8 位编码（通过`QTextCodec::codecForLocale()`获取）同时用于读取和写入。对于美国和西方区域（locale），这通常意味着 Latin-1。

如果我们设计了文件格式并希望能够读取和写入任意的 Unicode 字符，可以通过调用以下代码将数据保存为 Unicode：

```cpp
stream.setCodec("UTF-16");
stream.setByteOrderMark(true);
```

在开始写入之前，数据将以 UTF-16 格式保存，这每个字符需要两个字节，并以一个 16 位的值前缀（Unicode 字节序标记，`0xFFFE`），标识该文件为 Unicode 格式以及字节是小端序还是大端序。UTF-16 格式与`QString`的内存表示相同，因此在 UTF-16 中读取和写入 Unicode 字符串可以非常快。另一方面，在 UTF-16 格式下保存 ASCII 数据存在固有的开销，因为它为每个字符存储了两个字节而不是一个。

可以通过调用带有适当`QTextCodec`的`codec()`来指定其他编码。`QTextCodec`是一个在 Unicode 和编码之间转换的对象。Qt 在多种上下文中使用`QTextCodec`。在内部，它们被用于支持字体、输入法、剪贴板、拖放和文件名。但当我们编写 Qt 应用程序时，也可以使用它们。

在读取文件时，如果文件以字节序开头，`QTextStream`会自动检测 UTF-16。这种行为可以通过调用`setAutoDetectUnicode(false)`来关闭。如果数据是 UTF-16 但不能假设它以字节序开头，最好最好在读取之前调用`setCodec("UTF-16")`。

另一种支持整个 Unicode 的编码是 UTF-8。它相比 UTF-16 的主要优势是 ASCII 的超集。`0x00`到`0x7F`范围内的任何字符都表示为单字节。其他字符（包括`0x7F`以上的 Latin-1 字符）由多字节序列表示。对于大部分 ASCII，UTF-8 占据的空间约为 UTF-16 的一半。要在`QTextStream`中使用 UTF-8，在读写之前调用`setCodec("UTF-8")`作为编码名称。

如果我们希望无论用户的区域设置都读取和写入 Latin-1，我们可以在`QTextStream`上设置 ISO 8859-1 编码。例如：

```cpp
QTextStream in(&file);
setCodec("ISO 8859-1");
```

某些格式在文件头中指定其编码。文件头通常是纯 ASCII，以确保无论使用什么编码都能正确读取（假设它是 ASCII 的超集）。XML 文件格式就是一个有趣的例子。XML 文件通常被编码为 UTF-8 或 UTF-16。读取它们的正确方法是调用`setCodec("UTF-8")`。如果格式是 UTF-16，`QTextStream`会自动检测并调整。XML 文件的`<?xml?>`头部包含一个编码参数，例如：

```xml
<xml version="1.0" encoding="EUC-KR">
```

由于`QTextStream`不允许我们在开始读取后更改编码，指定显式编码的正确方法是重新开始读取文件，使用`setCodec`（从`QTextStream::codecName()`获取）。在 XML 的情况下，我们可以通过第 16 章中的 Qt XML 类来避免自己处理编码。

`QTextCodec`的另一个用途是指定源代码中出现的字符串的编码。让我们考虑，一个日本程序员组成的团队正在编写一个主要目标为日本本土市场的应用程序。这些程序员可能会在一个使用 EUC-JP 或 Shift-JIS 的文本编辑器中编写源代码。这种编辑器允许他们无缝地输入日语字符，以便编写如下代码：

```cpp
QPushButton *button = new QPushButton(tr("
```

默认情况下，`tr()`将参数解释为 Latin-1。要更改此，使用`QTextCodec::setCodecFor()`静态函数。例如：

```cpp
QTextCodec::setCodecFor(QTextCodec::codecName("EUC-JP"));
```

这必须在第一次调用`tr()`之前完成。通常，我们在`main()`中这样做，在调用`QCoreApplication`或`QApplication`之后。程序中的其他字符串仍将被解释为 Latin-1。如果程序员也想在这些地方输入日语字符，可以使用`QTextCodec`将它们显式转换为 Unicode：

```cpp
QString text = codec->toUnicode("
```

或者，我们可以通过调用`setCodecForCString(QTextCodec::codecName("EUC-JP"))`在转换`const char *`和`QString`时使用特定的编码。

上述技术适用于任何非语言，包括中文、希腊语和俄罗斯语。以下是 Qt 4.3 支持的编码列表：

- Apple Roman
- ISO 8859-5
- Ascii-M
- UTF-8
- Big5
- ISO 8859-6
- Ascii-Ori
- UTF-16
- Big5-HKSCS
- ISO 8859-7
- Ascii-Pnj
- UTF-16BE
- EUC-JP
- ISO 8859-8
- Ascii-Tlg
- UTF-16LE
- EUC-KR
- ISO 8859-9
- Ascii-Tml
- Windows-1250
- GB18030
- ISO 8859-10
- JIS X 0201
- Windows-1251
- IBM 850
- ISO 8859-13
- JIS X 0208
- Windows-1252
- IBM 866
- ISO 8859-14
- KOI8-R
- Windows-1253
- IBM 874
- ISO 8859-15
- KOI8-U
- Windows-1254
- ISO 2022-JP
- ISO 8859-16
- MuleLao-1
- Windows-1255
- ISO 8859-1
- Ascii-Bng
- ROMAN
- Windows-1256
- ISO 8859-2
- Ascii-Dev
- Shift-JIS
- Windows-1257
- ISO 8859-3
- Ascii-Gjr
- JIS-620
- Windows-1258
- ISO 8859-4
- Ascii-Knd
- TSCII
- WINSAMI2

对于所有这些，`QTextCodec::codecForName()`将始终返回一个有效指针。其他编码可以通过派生`QTextCodec`支持。

## 使应用程序支持翻译

如果我们希望我们的应用程序支持多种语言，我们必须做两件事：

- 确保每个用户可见的字符串都通过`tr()`
- 在启动时加载翻译文件 (`.qm`)

这两点都不适用于永远不会翻译的应用程序。然而，使用`tr()`需要一些精力，并为日后的翻译留下了可能。

# 18. 国际化

`tr()`函数是定义在`QObject`中的静态函数并在每个使用`Q_OBJECT`定义的子类中被重写。在`QObject`子类内部编写代码时，我们可以无正式地调用`tr()`。如果可用，`tr()`调用返回翻译；否则返回原始文本。在`QObject`子类内部，我们既可以使用带有类前缀的`QObject::tr`，也可以使用`DECLARE_TR_FUNCTIONS()`宏将`tr()`添加到类中，如第 8 章第 200 页所示。为了准备翻译文件，我们必须运行 Qt 的更新工具。该工具提取所有出现在`tr()`中的字符串字面量，并产生包含这些待翻译字符串的翻译文件。然后可以将这些文件发送给翻译人员添加翻译。该过程在本章后面的“翻译应用程序”部分进行解释。

`tr()`有以下通用语法：

```cpp
Context::tr(sourceText, comment)
```

`Context`部分是使用`Q`宏定义的`QObject`子类的名称。如果我们从相关类的成员函数中调用`tr()`，则不需要指定它。`sourceText`是需要翻译的字符串字面量。`comment`部分是可选的；它可以向翻译人员提供额外信息。

这里有几个示例：

```cpp
RockyWidget::QWidget(QWidget *parent)
    : QWidget(parent)
{
    QString str1 = tr("Letter")
    QString str2 = RockyWidget::tr("Letter")
    QString str3 = SnazzyDialog::tr("Letter")
    QString str4 = SnazzyDialog::tr("Letter", "US paper size");
}
```
