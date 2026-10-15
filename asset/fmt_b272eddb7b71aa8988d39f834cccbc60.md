
由于用户正在输入文本，提供键盘界面来更改文本格式是自然的。我们已将 `Ctrl+B` 设置为切换粗体，`Ctrl+I` 设置为切换斜体，`Ctrl+U` 设置为切换下划线。此外，`Ctrl+K` 调用颜色菜单，`Ctrl+M` 调用文本特效菜单（除了通过上下文菜单事件调用外）。通过对我们自行处理的按键调用 `accept()`，我们表明不需要对这些按键进行进一步的事件处理。

如果用户按下 Return 键，我们会发出 `returnPressed()` 信号，因为这可能很有用；文本中不会插入新行。其他按键传递到基类。`QTextEdit` 类支持其自己的按键序列——例如，`Ctrl+左箭头` 向左移动一个单词，`Ctrl+Del` 删除右侧的单词，`Ctrl+C` 将选定的任何文本复制到剪贴板，以及当然的简单字母，如 a、b、Shift+A 和 Shift+B，它们会被直接插入。

```python
def toggleBold(self):
    self.setFontWeight(QFont.Normal \
if self.fontWeight() > QFont.Normal else QFont.Bold)
```

PyQt 支持多种粗度级别，但我们选择采用简单的粗体开/关方法。`QTextEdit.fontWeight()` 方法返回当前插入点处的字体粗细，类似地，`setFontWeight()` 方法应用于当前插入点或选中的文本。`QTextEdit` 在格式化方面相当智能，至少在线 Linux 上是这样。例如，如果文本被选中，格式化仅应用于选区；如果没有选区且插入点位于文本末尾，格式化应用于该点之后的部分；如果没有选区且插入点位于单词中间，格式化应用于整个单词。

```python
def toggleItalic(self): 
    self.setFontItalic(not self.fontItalic())

def toggleUnderline(self): 
    self.setFontUnderline(not self.fontUnderline())
```

斜体 和 下划线 都是简单的开/关设置，在 Linux 上，切换它们的工作方式与应用粗体或其他格式化的智能方式相同。

```python
def colorMenu(self): 
    pixmap = QPixmap(22, 22) 
    menu = QMenu("Color") 
    for text, color in (("$Black", Qt.black), ("$Blue", Qt.blue), 
                        ("$Dark Blue", Qt.darkBlue), ("$Cyan", Qt.cyan), 
                        ("$Dark Cyan", Qt.darkCyan), ("$Green", Qt.green), 
                        ("$Dark Green", Qt.darkGreen), 
                        ("$Magenta", Qt.magenta), 
                        ("$Dark Magenta", Qt.darkMagenta), 
                        ("$Red", Qt.red), ("$Dark Red", Qt.darkRed)): 
        color = QColor(color) 
        pixmap.fill(color) 
        action = menu.addAction(QIcon(pixmap), text, self.setColor) 
        action.setData(QVariant(color)) 
    self.ensureCursorVisible() 
    menu.exec_(self.viewport(), mapToGlobal(self.cursorRect().center())) 
```

颜色菜单由 `Ctrl+K` 调用。为了创建菜单，我们遍历一个文本和颜色常量的列表，为每个常量添加一个新的菜单选项。我们将每个动作的数据设置为相关的颜色；我们在 `setColor()` 的实现中使用这些数据。

我们希望菜单在插入点处弹出，即在文本光标位置。这并不一定直截了当，因为 RichTextLineEdit 可能包含比其显示宽度更多的文本，且插入点可能位于可见区域之外。

我们通过做两件事来解决这个问题。首先，我们调用基类的 `QTextEdit.ensureCursorVisible()` 方法；这会使编辑器滚动，从而使插入点位于可见区域内——如果插入点已经可见，则不执行任何操作。其次，我们在插入点矩形的中心弹出菜单。`cursorRect()` 方法返回一个以控件坐标为单位的 `QRect`，因此我们必须相应地转换从 `QRect.center()` 获取的 `QPoint` 的坐标。我们通过调用 `viewport()` 来实现这一点，它实际上返回一个具有可见区域确切尺寸并知道其代表编辑器哪个区域的控件。然后我们使用视口控件的 `mapToGlobal()` 方法将点从控件坐标系转换为 `QMenu.exec_()` 用于定位的全局（屏幕）坐标系。

```python
def setColor(self):
    action = self.sender()
    if action is not None and isinstance(action, QAction):
        color = QColor(action.data())
        if color.isValid():
            self.setTextColor(color)
```

如果用户选择了一种颜色，就会调用 `setColor()` 方法。我们检索存储在调用动作用户数据中的颜色，并将该颜色应用于文本。同样，应用 粗体、斜体 和下划线所使用的相同逻辑也用于将颜色应用于选定的文本、当前单词或从文本末尾开始的部分。

```python
def textEffectMenu(self):
    format = self.currentCharFormat()
    menu = QMenu("Text Effect")
    for text, shortcut, data, checked in (
        ("$Bold", "Ctrl+B", RichTextLineEdit.Bold,
         self.fontWeight() > QFont.Normal),
        ("$Italic", "Ctrl+I", RichTextLineEdit.Italic,
         self.fontItalic()),
        ...
        ("$Subscript", None, RichTextLineEdit.Subscript,
         format.verticalAlignment() == \
         QTextCharFormat.AlignSubScript),
    ):
        action = menu.addAction(text, self.setTextEffect)
        if shortcut is not None:
            action.setShortcut(QKeySequence(shortcut))
        action.setData(QVariant(data))
        action.setCheckable(True)
        action.setChecked(checked)
    self.ensureCursorVisible()
    menu.exec_(self.viewport().mapToGlobal(
        self.cursorRect().center()))
```

由 `Ctrl+M` 或上下文菜单事件调用的文本特效菜单方法，在结构上与颜色菜单方法相似，但稍显复杂。

我们首先获取当前生效的文本格式，因为我们需要此信息来确定是否要检查各个菜单选项。然后，我们使用由四元组（文本、快捷键、常量、勾选状态）组成的列表创建一个菜单。菜单如图 13.3 所示。

![](img/9bfe0a027fcc8793bb087287001100dd_408_0.png)

我们为某些操作设置了键盘快捷键——例如，粗体使用 Ctrl+B。我们没有使用标准化的按键序列，因为我们在前面展示的就键按压事件处理器中硬编码了按键操作，所以必须确保与处理器期望的按键匹配。
