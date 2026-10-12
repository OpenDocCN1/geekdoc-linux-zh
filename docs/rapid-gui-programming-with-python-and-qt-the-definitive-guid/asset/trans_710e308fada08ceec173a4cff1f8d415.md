
## 第 386 页 第 13 章。富文本与打印

`event()` 处理器在任何特定的键盘或鼠标事件处理器之前被调用，也是我们唯一可以拦截并处理 Tab 键按下的地方。如果用户按下了 Tab 键，我们会从 `QTextEdit` 获取一个 `QTextCursor`；这允许我们以编程方式与底层持有文本的 `QTextDocument` 进行交互。默认情况下，由文本编辑框返回的文本光标位于当前插入点（也称为光标位置），因此我们可以简单地插入四个空格。然后我们返回 `True`，以告知事件处理系统我们已经处理了 Tab 键按下事件，并且不应采取进一步的操作（例如改变焦点）。

为了提供语法高亮，我们必须创建一个 `QSyntaxHighlighter` 子类，实现 `highlightBlock()` 方法，并创建一个高亮器实例，将其要应用的 `QTextDocument` 作为参数。我们已经在 `MainWindow` 的初始化程序中完成了最后部分，所以现在我们将转向我们的 `QSyntaxHighlighter` 子类。

`QSyntaxHighlighter` 基于逐行工作，并提供了一种简单的跨多行跟踪状态的手段。对于 Python 编辑器，我们将使用正则表达式来识别 Python 关键字、注释和字符串（包括跨越多行的三引号字符串），以便对它们应用高亮。我们首先从在子类初始化程序中设置正则表达式开始，我们将分两部分来看。

```python
class PythonHighlighter(QSyntaxHighlighter):
    Rules = []
    def __init__(self, parent=None):
        super(PythonHighlighter, self).__init__(parent)
        keywordFormat = QTextCharFormat()
        keywordFormat.setForeground(Qt.darkBlue)
        keywordFormat.setFontWeight(QFont.Bold)
        for pattern in (r"\b\w\d", r"\b\w", r"\b\w", ...):
            ... 
        PythonHighlighter.Rules.append((QRegExp(pattern), keywordFormat))
```

静态列表 `Rules` 保存了一个配对列表。每个配对中的第一个元素是一个正则表达式（一个 `QRegExp`），用于匹配只能占据单行的语法结构（例如 Python 关键字）。第二个元素是一个 `QTextCharFormat`，这是一个可以保存文本片段格式信息的对象，例如它的字体以及应使用什么画笔来绘制它。

我们为每个 Python 关键字创建了一个规则，赋予它们相同的 `keywordFormat` 格式。（由于省略号所示，片段中未显示大多数关键字。）每个关键字前后都有 `\b`；这是一个正则表达式符号，它不匹配任何文本，而是匹配词边界。这意味着，例如，在表达式 **a and b** 中，`and` 将被识别为关键字，而在表达式 **a = sand** 中，**sand** 中的 `and` 将（正确地）不被识别。

```python
commentFormat = QTextCharFormat()
commentFormat.setForeground(QColor(0, 127, 0))
commentFormat.setFontItalic(True)
PythonHighlighter.Rules.append((QRegExp(r"#.*"),
                commentFormat))

self.stringFormat = QTextCharFormat()
self.stringFormat.setForeground(Qt.darkYellow)
stringRe = QRegExp(r"""([\"'].*[\"'])""")
stringRe.setMinimal(True)
PythonHighlighter.Rules.append((stringRe, self.stringFormat))
self.stringRe = QRegExp(r"""(:[\"']*.\"'",.*?)""")
self.stringRe.setMinimal(True)
PythonHighlighter.Rules.append((self.stringRe,
             self.stringFormat))
self.tripleSingleRe = QRegExp(r"""'''""")
self.tripleDoubleRe = QRegExp(r""""""""")
```

在关键字之后，我们为处理 Python 注释创建了一个格式和正则表达式。该正则表达式并不完美；它例如没有考虑引号内的 # 字符。

对于字符串，我们将字符串格式保留为实例变量，因为我们需要在 `highlightBlock()` 方法中处理多行字符串时使用它。单行字符串由初始化程序中设置的简单（但快速）正则表达式处理，并添加到 `Rules` 列表中。最后我们创建了两个额外的正则表达式。这两个都使用负向前瞻；例如，`(?!)` 意味着“后面不跟有空格”。它们用于 `highlightBlock()` 方法，我们将在下一部分分两部分回顾该方法。

```python
def highlightBlock(self, text):
    NORMAL, TRIPLESINGLE, TRIPLED_DOUBLE = range(3)
    for regex, format in PythonHighlighter.Rules:
        i = text.indexOf(regex)
        while i >= 0:
            length = regex.matchedLength()
            self.setFormat(i, length, format)
            i = text.indexOf(regex, i + length)
```

`highlightBlock()` 方法为每一行显示的内容调用，该行位于第 0 个字符串参数 `text` 中。

我们首先设置三种可能的状态：正常、在三引号字符串内、在三双引号字符串内。然后我们遍历每个规则，并找到匹配规则正则表达式的位置，我们将文本格式设置为该正则表达式匹配长度对应的格式。正则表达式和格式对的列表以及前面代码中显示的 for 循环的组合，对于所有语法组件只占据单行且每个都能用正则表达式表示的语法高亮都是足够的。

```python
self.setCurrentBlockState(NORMAL)
if text.indexOf(self.stringQ) != -1:
    return
for i, state in ((text.indexOf(self.tripleSingleRe),
                  TRIPLESINGLE),
                 (text.indexOf(self.tripleDoubleRe),
                  TRIPLED_DOUBLE)):
    if self.previousBlockState() == state:
        if i == -1:
            i = text.length()
        self.setCurrentBlockState(state)
        self.setFormat(0, i + 3, self.stringFormat)
    elif i > -1:
        self.setCurrentBlockState(state)
        self.setFormat(i, text.length(), self.stringFormat)
```

接下来我们将当前块的状态设置为正常。该状态是我们选择的整数，`QSyntaxHighlighter` 会将其与当前行关联。然后我们测试是否有一个完整的三引号字符串，即在同一行开始和结束；如果是，我们已经格式化过了，所以结束并返回。

在 PyQt 的文本处理类（如 `QTextDocument`、`QTextEdit` 和 `QSyntaxHighlighter`）中，文本块本质上是由换行符分隔的字符序列。对于文字处理类型文档，这等同于一个段落（因为文本处理类执行自动换行），但对于源代码，我们手动插入换行符，所以在这种情况下，每个块实际上是一行代码。

我们现在需要处理三种情况。要么我们处于一个从之前行开始且在本行未结束的三引号字符串中；要么我们拥有本行中三引号字符串的开头或结尾。

如果前一行处于三引号字符串中且本行没有三引号，那么整行仍然处于三引号字符串中，所以我们设置当前块状态与前一行相同，并将整行格式化为三引号格式。如果前一行状态是三引号且我们有一个三引号，那必须是闭合的三引号，所以我们格式化到包括该三引号为止的三引号格式。在这种情况下，我们将状态保留为正常，因为这将从三引号字符串结束后的部分开始适用。另一方面，如果前一行状态不是三引号且我们发现三引号，我们将状态设置为三引号，并从这些引号开始格式化到行尾。

这完成了我们的语法高亮示例。显然，我们可以使用更复杂的正则表达式，甚至完全避免使用它们，而是使用有限状态自动机或解析器来识别每行中需要特定格式的部分。对于具有复杂语法的大型文本，语法高亮在计算上可能开销很大，但 `QSyntaxHighlighter` 通过仅格式化足够多的行以正确高亮可见行，帮助降低开销。

### 富文本单行编辑框

在某些应用程序中，要求用户能够输入单行富文本。例如，数据库应用程序可能有一个“描述”字段，如果我们希望用户可以使用粗体、斜体和颜色来强调特定单词。我们将在第 14 章和第 16 章中看到此类示例。不幸的是，PyQt 没有提供这样的控件。在本小节中，我们将创建一个 `RichTextLineEdit`，它是 `QTextEdit` 的一个子类，提供我们所需的功能；它如图 13.2 所示。在此过程中，我们将学习如何以编程方式格式化 `QTextEdit` 中的文本片段，以及如何迭代 `QTextEdit` 的 `QTextDocument` 以提取文本及其格式。

![](img/9bfe0a027fcc8793bb087287001100dd_403_0.png)

**图 13.2** *富文本单行编辑框*

富文本单行编辑框将支持适用于单行文本的最常见的文本格式类型：粗体、斜体、下划线、删除线、上标和下标。此外，将支持三种字体样式——等宽、无衬线和衬线——以及将文本颜色设置为有限范围颜色的能力。我们将从一些静态常数和初始化程序开始。

```python
class RichTextLineEdit(QTextEdit):
    (Bold, Italic, Underline, StrikeOut, Monospaced, Sans, Serif,
     NoSuperOrSubscript, Subscript, Superscript) = range(10)

    def __init__(self, parent=None):
        super(RichTextLineEdit, self).__init__(parent)
        self.monofamily = QString("courier")
        self.sansfamily = QString("helvetica")
        self.serifamily = QString("times")
        self.setLineWrapMode(QTextEdit.NoWrap)
        self.setTabChangesFocus(True)
        self.setVerticalScrollBarPolicy(Qt.ScrollBarAlwaysOff)
        self.setHorizontalScrollBarPolicy(Qt.ScrollBarAlwaysOff)
        fm = QFontMetrics(self.font())
        h = int(fm.height() * (1.4 if platform.system() == "Windows" \
                              else 1.2))
```
