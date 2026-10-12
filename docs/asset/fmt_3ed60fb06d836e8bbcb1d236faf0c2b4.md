
实际上，这些快捷键在实践上并没有效果，因为它们只存在于与其关联的操作的生命周期内，而操作只在菜单存在时（即 `textEffectMenu()` 方法的执行期间）才存在。但这并不重要，因为我们已经重新实现了按键事件处理器，以提供这些快捷键。菜单中的快捷键仅对永久性菜单（例如添加到主窗口菜单栏的菜单）有用。那么，为什么我们还要在菜单中费心设置快捷键呢？因为添加快捷键会让它们显示在菜单中，从而帮助用户了解这些快捷键。这并没有解决用户最初如何得知 `Ctrl+M` 和 `Ctrl+K` 菜单的问题，但希望用户能看到工具提示或在应用程序手册中阅读到相关内容。

菜单本身的创建和弹出方式与颜色菜单完全相同。如果用户点击任何文本效果选项，就会调用 `setTextEffect()` 方法。我们将分两部分来看待这个方法。

```python
def setTextEffect(self):
    action = self.sender()
    if action is not None and isinstance(action, QAction):
        what = action.data().toInt()[0]
        if what == RichTextLineEdit.Bold:
            self.toggleBold()
        return
    if what == RichTextLineEdit.Italic:
        self.toggleItalic()
    return
    if what == RichTextLineEdit.Underline:
        self.toggleUnderline()
    return
```

每个文本效果菜单操作都在其用户数据中存储了一个常量；该常量被检索并保存在 `what` 变量中。对于简单的切换操作，我们只需调用相应的切换方法即可。

```python
format = self.currentCharFormat()
if what == RichTextLineEdit.Monospaced:
    format.setFontFamily(self.monofamily)
elif what == RichTextLineEdit.Serif:
    format.setFontFamily(self.seriffamily)
elif what == RichTextLineEdit.Sans:
    format.setFontFamily(self.sansfamily)
if what == RichTextLineEdit.StrikeOut:
    format.setFontStrikeOut(not format.fontStrikeOut())
if what == RichTextLineEdit.NoSuperOrSubscript:
    format.setVerticalAlignment(QTextCharFormat.AlignNormal)
elif what == RichTextLineEdit.Superscript:
    format.setVerticalAlignment(QTextCharFormat.AlignSuperScript)
elif what == RichTextLineEdit.Subscript:
    format.setVerticalAlignment(QTextCharFormat.AlignSubScript)
self.mergeCurrentCharFormat(format)
```

要更改字体族、删除线格式或垂直对齐方式，我们必须检索当前格式，应用用户请求的更改，然后将更新的格式与当前格式合并，使其生效。

现在我们已经涵盖了富文本行编辑支持的所有格式选项。一旦用户输入了富文本，我们无疑想要检索它以进行存储、搜索或操作。我们可以使用 `QTextEdit.toPlainText()` 方法——但这会剥离所有 HTML，结果与我们使用 `QLineEdit` 没有什么两样。更合适的替代方案是使用 `QTextEdit.toHtml()`，但此方法返回的 HTML 相当冗长，因为它必须足够通用，以涵盖 PyQt 支持的所有 HTML 标签。

为了说明这一点，如果我们有一段文本“The **bold** cat.”（13 个字符），其中单词“bold”为粗体，单词“cat”为红色，那么 `toHtml()` 方法将返回 503 个字符：

```html
<html><head><meta name="qrichtext" content="1" />
<style type="text/css"> p, li { white-space: pre-wrap; } </style>
</head>
<body style=" font-family:'Nimbus Sans L'; font-size:11pt;
font-weight:400; font-style:normal; text-decoration:none;">
<p style=" margin-top:0px; margin-bottom:0px; margin-left:0px;
margin-right:0px; -qt-block-indent:0; text-indent:0px;">The
<span style=" font-weight:600;">>bold</span>
<span style=" color:#ff0000;">>cat</span></p>
<span style=" color:#00000;">>,</span></p></body></html>
```

我们添加了一些换行符，以使输出能整齐地排列在页面上。文本可能会因平台和 Qt 版本的不同而略有差异，但其长度仍将约为 500 个字符。由于富文本行编辑只需要支持有限的标签子集，因此可以使用更简单的 HTML。例如：

```html
The <b>bold</b><font color="#ff0000">cat</font>
```

这仅仅有 49 个字符。为了实现这种更简单的 HTML 格式，我们提供了一个 `toSimpleHtml()` 方法；它有点长，因此我们将分三部分回顾它。

```python
def toSimpleHtml(self):
    html = QString()
    black = QColor(Qt.black)
    block = self.document().begin()
```

我们首先创建一个空的 `QString` 目标，并假设文本颜色为黑色。由 `QTextEdit.document()` 返回的 `QTextDocument` 类提供了一种遍历文本及其包含的格式的方法。基本上，每个主要的文本组件（如段落或表格）都包含在一个“块”中，我们可以使用 `QTextDocument.begin()` 检索第一个块，并使用 `QTextBlock.next()` 检索后续的每个块。空文档将有一个无效的起始块。

每个文本块包含一个或多个文本“片段”，每个片段都有其自身的格式特征。实际上，`QTextDocument` 的结构比这更复杂，但我们可以忽略额外的细节，如表格、列表和图片，因为它们在富文本行编辑中并未使用。

```python
while block.isValid():
    iterator = block.begin()
    while iterator != block.end():
        fragment = iterator.fragment()
        if fragment.isValid():
            format = fragment.charFormat()
            family = format.fontFamily()
            color = format.foreground().color()
            text = Qt.escape(fragment.text())
```
