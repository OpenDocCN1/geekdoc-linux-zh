
- `ISO 8859-4`
- `ISO 8859-5`
- `ISO 8859-6`
- `ISO 8859-7`
- `ISO 8859-8`
- `ISO 8859-9`
- `ISO 8859-10`
- `ISO 8859-13`
- `ISO 8859-14`
- `ISO 8859-15`
- `ISO 8859-16`
- `Iscii-Bng`
- `Iscii-Dev`
- `Iscii-Gjr`
- `Iscii-Knd`
- `Iscii-Mlm`
- `Iscii-Ori`
- `Iscii-Pnj`
- `Iscii-Tlg`
- `Iscii-Tml`
- `JIS X 0201`
- `JIS X 0208`
- `KOI8-R`
- `KOI8-U`
- `MuleLao-1`
- `ROMAN8`
- `Shift-JIS`
- `TIS-620`
- `TSCII`
- `UTF-8`
- `UTF-16`
- `UTF-16BE`
- `UTF-16LE`
- `Windows-1250`
- `Windows-1251`
- `Windows-1252`
- `Windows-1253`
- `Windows-1254`
- `Windows-1255`
- `Windows-1256`
- `Windows-1257`
- `Windows-1258`
- `WINSAMI2`

对于所有这些编码，`QTextCodec::codecForName()` 始终返回一个有效指针。可以通过子类化 `QTextCodec` 支持其他编码。

## 第三部分：高级 Qt

## 18. 国际化

![](img/1bc72df8c60cf85926d3aefcc273027d_672_0.png)

- 使用 Unicode
- 使应用程序具备翻译感知能力
- 动态语言切换
- 翻译应用程序

除了用于英语和许多欧洲语言的拉丁字母表外，Qt 4 还对世界上其他文字系统提供了广泛支持：

Qt 在整个 API 和内部都使用 Unicode。无论我们使用什么语言的用户界面，应用程序都能平等地支持所有用户。Qt 的文本引擎可以处理所有主要的非拉丁文字系统，包括阿拉伯语、中文、西里尔语、韩语和日语。Qt 的布局引擎支持阿拉伯语和希伯来语等从右向左的布局。某些语言需要特殊的输入法来输入文本。`QLineEdit` 和 `QTextEdit` 等小控件可以很好地配合系统中安装的任何输入法。通常，让用户输入母语是不够的；整个用户界面必须翻译。Qt 使这变得简单：只需将所有可见字符串封装在 `tr()` 函数中（正如我们在前面的章节中所做的），并使用 Qt 的工具准备翻译文件。Qt 提供了一个名为 Linguist 的 GUI 工具供翻译人员使用。Linguist 还由两个命令行程序 `lupdate` 和 `lrelease` 补充。对于大多数应用程序，启动时根据区域设置加载翻译文件。但在少数情况下，用户需要在运行时切换语言。这完全可行，尽管需要一些额外工作。得益于 Qt 的布局系统，当翻译文本比原始文本长时，各种用户界面组件会自动调整。

### 使用 Unicode

Unicode 是一种支持世界上大多数文字系统的字符编码标准。Unicode 的原始思想是，使用 16 位而不是 8 位来存储字符，就可以编码 65536 个字符而不是只有 256 个。Unicode 与 ASCII 以及 ISO 8859-1 (Latin-1) 子集在相同的位置包含字符。例如，字符 'A' 在 ASCII、Latin-1 和 Unicode 中的值均为 0x41，而字符 'Ñ' 在 Latin-1 和 Unicode 中的值为 0xD1。Unicode 标准分配了 65535 以上的数值。这些字符可以使用被称为“代理对”（surrogate pairs）的两个16位序列表示。Qt 的 `QString` 类将字符串存储为 Unicode。`QString` 中的每个字符都是 16 位的 `QChar`，而不是 8 位的 `char`。以下设置字符串第一个字符为 'A' 的两种方法：

```cpp
str[0] = 'A';
str[0] = QChar(0x41);
```

如果源文件以 Latin-1 编码，指定 Latin-1 字符同样简单：

```cpp
str[0] = 'Ñ';
```

如果源文件有其他编码，数值方法同样有效：

```cpp
str[0] = QChar(0xD1);
```

我们可以通过数值指定任何 Unicode 字符。例如，这里是指定希腊大写字母 sigma ![](img/1bc72df8c60cf85926d3aefcc273027d_673_0.png)) 和欧元货币符号 ('€') 的方法：

```cpp
str[0] = QChar(0x3A3);
str[0] = QChar(0x2AC);
```

Unicode 支持的所有字符的数值列在 http://www.unicode.org/standard/。如果你很少需要非 Latin-1 的 Unicode 字符，在线查找字符足够了；但 Qt 更方便的方法在 Qt 程序中输入 Unicode 字符串，正如本节后面所示。

Qt 4 的文本引擎在所有平台上都支持以下文字系统：阿拉伯语、中文、西里尔语、希腊语、日语、韩语、老、泰语和越南语。它还支持所有不需要特殊处理的 Unicode 4.1 脚本。此外，在带有 Fontconfig 的 X11 和最新版本的 Windows 上支持以下文字系统：孟加拉语、天城罗文、古吉拉特语、旁遮普语、坎纳达语、高棉语、马拉马拉拉姆语、叙利亚语、泰米卢语、泰卢固语、Thaana（迪维语）和西藏语。最后，X11 支持奥里亚语，Windows XP 支持蒙古语和辛哈罗拉语。假设系统中安装了正确的字体，Qt 可以使用这些文字系统之一渲染文本。假设安装了正确的输入法，用户将在他们的 Qt 应用程序中输入这些文字系统的文本。

使用 `QChar` 编程与使用 `char` 略有不同。要获取 `QChar` 的数值，对其调用 `unicode()`。要获取 `QChar` 的 ASCII 或 Latin-1 值（作为 `char`），调用 `toLatin1()`。对于非 Latin-1 字符，`toLatin1()` 返回 `'\0'`。

如果我们知道程序中的所有字符串都是 ASCII，我们对 `toLatin1()` 的返回值可以使用标准的 `<cctype>` 函数，如 `isalpha()`、`isdigit()` 和 `isspace()`。然而，通常使用 `QChar` 的成员函数来执行这些操作更好，因为它们适用于任何 Unicode 字符。`QChar` 提供的函数包括 `isPrint()`、`isPunct()`、`isSpace()`、`isMark()`、`isLetter()`、`isNumber()`、`isLetterOrNumber()`、`isDigit()`、`isSymbol()`、`isLower()` 和 `isUpper()`。例如，这里测试字符是否为数字或大写字母的一种方法：

```cpp
if (ch.isDigit() || ch.isUpper())
...
```

此代码段适用于任何区分大写和小写的字母表，包括拉丁字母、希腊字母和西里尔字母。

一旦我们有了 Unicode 字符串，我们可以在 Qt API 中任何期望 `QString` 的地方使用它。此时，Qt 的职责是正确显示它，并在与操作系统通信时将其转换为相关的编码。

在读写文本文件时需要特别注意。文本文件可以使用多种编码，通常无法从内容推测文本文件的编码。默认情况下，`QTextStream` 使用系统的本地 8 位编码（通过 `QTextCodec::codecForLocale()` 可用）进行读取和写入。对于美国和西欧区域，这通常意味着 Latin-1。

如果我们设计了自己的文件格式，并希望能够读写任意 Unicode 字符，可以通过调用以下代码将数据保存为 Unicode：

```cpp
stream.setCodec("UTF-16");
stream.setGenerateByteOrderMark(true);
```

在我们开始向 QTextStream 写入数据之前。数据将被保存为 UTF-16 格式，这种格式每个字符需要两个字节，并且会以一个特殊的 16 位值（Unicode 字节序标记，0xFFFE）开头，用于标识该文件是否为 Unicode 格式以及字节是小端序还是大端序。UTF-16 格式与 QString 的内存表示相同，因此在 UTF-16 中读写 Unicode 字符串可以非常快。另一方面，使用 UTF-16 格式保存纯 ASCII 数据时存在固有的开销，因为每个每个字符都存储了两个字节而不是一个字节。

可以通过调用 `setCodec()` 并传入合适的 `QTextCodec` 来指定其他编码。`QTextCodec` 是一个在 Unicode 和给定编码之间转换的对象。Qt 在各种上下文中使用了 `QTextCodec`。在内部，它们被用于支持字体、输入法、剪贴板、拖放和文件名。但在我们编写 Qt 应用程序时，也可以使用它们。

在读取文本文件时，如果文件以字节序标记开头，`QTextStream` 会自动检测 UTF-16。这种行为可以通过调用 `autoDetectUnicode(false)` 来关闭。如果数据是 UTF-16 但无法假设它以字节序标记开头，最好在读取之前调用 `setCodec("UTF-16")`。

另一种支持整个 Unicode 的编码是 UTF-8。它相比 UTF-16 的主要优势是它是 ASCII 的超集。0x00 到 0x7F 范围内的任何字符都表示为单字节。其他字符（包括 0x7F 以上的 Latin-1 字符）用多字节序列表示。对于大部分是 ASCII 的文本，UTF-8 占用空间大约是 UTF-16 的一半。要在 QTextStream 中使用 UTF-8，请在读写之前调用 `setCodec("UTF-8")` 指定编码名称。

如果我们无论用户的区域设置如何，都始终想读写 Latin-1，我们可以在 QTextStream 上设置 "ISO 8859-1" 编码。例如：

```cpp
QTextStream in(&file);
in.setCodec("ISO 8859-1");
```

某些文件格式会在其头部信息中指定编码。头部通常是纯 ASCII，以确保无论使用什么编码都能被正确读取（假设它是 ASCII 的超集）。XML 文件格式就是一个趣的例子。XML 文件通常被编码为 UTF-8 或 UTF-16。读取它们的正确方法是调用 `setCodec("UTF-8")`。如果格式是 UTF-16，`QTextStream` 将自动检测到这一点并调整自身。XML 文件的 `<?xml?>` 头部有时包含编码参数，例如：

```xml
<?xml version="1.0" encoding="EUC-KR"?>
```

由于 `QTextStream` 不允许在开始读取后更改编码，因此遵循显式编码正确方法是重新开始读取文件，使用正确的编码器（通过 `QTextCodec::codecForName()` 获取）。在 XML 的情况下，通过使用第 16 章描述的 Qt XML 类，我们可以避免亲自处理编码。

`QTextCodec` 的另一个用途是指定源代码中出现字符串的编码。让我们考虑一个例子，一个主要针对日本本土市场的应用程序的日本程序员团队。这些程序员可能会在一个使用如 EUC-JP 或 Shift-JIS 等编码的文本编辑器中编写源代码。这种编辑器允许他们无缝地输入日语字符，以便他们编写如下代码：

```cpp
QPushButton *button = new QPushButton(tr(
    ![](img/1bc72df8c60cf85926d3aefcc273027d_676_0.png)
));
``` （注意：OCR 文本显示函数调用中有一个换行符）

默认情况下，Qt 将 `tr()` 的参数解释为 Latin-1。要更改此设置，请调用静态函数 `QTextCodec::setCodecForTr()`。例如：

```cpp
QTextCodec::setCodecForTr(QTextCodec::codecForName("EUC-JP"));
```

这必须在第一次调用 `tr()` 之前完成。通常，我们会在 `main()` 中、在创建 `QCoreApplication` 或 `QApplication` 对象后立即执行此。

程序中指定的其他字符串仍将被解释为 Latin-1 字符串。如果程序员还想在这些字符串中输入日语字符，他们可以使用 `QTextCodec` 将其显式转换为 Unicode：

```cpp
QString text = japaneseCodec->toUnicode(
    ![](img/1bc72df8c60cf85926d3aefcc273027d_676_1.png)
);
```

或者，他们可以通过调用 `QTextCodec::setCodecForCStrings()` 告诉 Qt 在 `const char *` 和 `QString` 之间转换时使用特定的编码：

```cpp
QTextCodec::setCodecForCStrings(QTextCodec::codecForName("EUC-JP"));
```

上述技术适用于任何非 Latin-1 语言，包括中文、希语、韩语和俄语。

以下是 Qt 4.3 支持的编码列表：

| | |
| :--- | :--- |
| Apple Roman | Big5 |
| Big5-HKSCS | EUC-JP |
| EUC-KR | GB18030 |
| IBM 850 | IBM 866 |
| IBM 874 | ISO 2022-JP |
| ISO 8859-1 | ISO 8859-2 |
| ISO 8859-3 | ISO 8859-4 |
| ISO 8859-5 | ISO 8859-6 |
| ISO 8859-7 | ISO 8859-8 |
| ISO 8859-9 | ISO 8859-10 |
| ISO 8859-13 | ISO 8859-14 |
| ISO 8859-15 | ISO 8859-16 |
| ISOII-B | ISOII-Dev |
| ISOII-G | ISOII-K |
| ISOII-M | ISOII-Ori |
| ISOII-P | ISOII-T |
| JIS X-0201 | JIS X0208 |
| KOI8-R | KOI8-U |
| Lao-1 | ROMAN8 |
| Shift-JIS | TIS-620 |
| TSCII | UTF-8 |
| UTF-16 | UTF-16BE / UTF-16LE |
| Windows-1250 | Windows-1251 |
| Windows-1252 | Windows-1253 |
| Windows-1254 | Windows-1255 |
| Windows-1256 | Windows-1257 |
| Windows-1258 | Windows-2 |

对于所有这些，`QTextCodec::codecForName()` 总是返回一个有效指针。可以通过子类 `QTextCodec` 支持其他编码。

## 18. 国际化

### 使应用程序具备翻译能力

动态切换

除了英语和许多欧洲语言使用的拉丁字母外，Qt 4 还对世界上其他文字系统提供了广泛支持：Qt 在整个 API 内部使用 Unicode。无论我们在用户界面使用什么语言，应用程序都可以支持。文本引擎可以处理所有主要的非拉丁文字系统，包括中文、希腊语、希伯来语、日语、韩语和印度的语言。布局引擎支持阿拉伯语和希伯来语等从右到左的布局。某些语言需要特殊的输入法来输入文本。`QLineEdit` 和 `QTextEdit` 等编辑器控件可以与系统中安装的任何输入法良好工作。

允许用户使用原生输入文本是不够的，整个用户界面也必须翻译。Qt 让这变得简单：只需用 `tr()` 函数封装所有可见字符串（如我们在前面的章节中所做），并使用 Qt 的工具准备所需语言的翻译文件。Qt 提供了一个名为 Linguist 的 GUI 工具供翻译人员使用。Qt Linguist 由两个命令行程序 `lupdate` 和 `lrelease` 补充，它们通常由应用程序的开发者运行。

对于大多数应用程序，根据用户的区域设置加载翻译文件。但在某些情况下，用户需要在运行时切换语言。这在 Qt 中完全可行，尽管需要一些额外工作。得益于 Qt 的布局系统，当翻译文本比原文长时，各种用户界面组件会自动调整以留出空间。

### 使用 Unicode

Unicode 是一种支持世界上大多数文字系统的字符编码标准。Unicode 的原始想法是，使用 16 位而不是 8 位来存储字符，可以编码 65000 个字符而不是 256 个。Unicode 在相同的代码位置包含 ASCII 和 ISO 8859-1 (Latin-1) 作为子集。例如，字符 'A' 在 ASCII、Latin-1 和 Unicode 中的值均为 0x41，字符 'Ñ' 在 Latin-1 和 Unicode 中的值均为 0xD1。Unicode 标准的新版本分配了 65535 以上的字符值。这些字符可以使用两个 16 位值的序列（代理对）来表示。

Qt 的 `QString` 类将字符串存储为 Unicode。`QString` 中的每个字符都是 16 位的 `QChar`而不是 8 位的 `char`。以下是设置字符串第一个字符为 'A' 的两种方法：

```cpp
str[0] = 'A';
str[0] = QChar(0x41);
```

如果源文件以 Latin-1 编码，指定 Latin-1 字符同样简单：

```cpp
str[0] = 'Ñ';
```

如果源文件有其他编码，数值值同样有效：

```cpp
str[0] = QChar(0xD1);
```

我们可以通过数值值指定任何 Unicode 字符。例如，这里是指定希腊大写字母 sigma ('![](img/1bc72df8c60cf85926d3aefcc273027d_681_0.png)') 和欧元货币符号 ('€') 的方法：
