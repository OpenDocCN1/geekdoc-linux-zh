
PyQt 最大且最持久的优势之一，就是创建自定义控件的便捷性。我们用 PyQt 创建的自定义控件与标准内置控件的制作方式相同，因此它们能够无缝集成，且在外观和行为方面没有任何任意限制。在 PyQt 中创建自定义控件并非“一刀切”。相反，我们可以从多种方法中选择，这些方法赋予了我们对控件行为和外观逐步增加的掌控力。

最基本的自定义级别是简单地设置现有控件的一些属性。我们在前面的章节中已经多次这样做过。例如，在前一章中，我们仅通过在我们的控件上调用 `setAcceptDrops(True)` 和 `setDragEnabled(True)` 就启用了 PyQt 的默认拖放行为。对于自旋框（spinboxes），我们可以限制其行为——例如，通过调用 `setRange()` 来设置最小值和最大值——并使用 `setPrefix()` 和 `setSuffix()` 来影响其外观。本章不会展示这种方法示例，因为我们在之前已经多次看到过它的实际运作。

如果设置现有控件的属性不足以完成自定义，我们可以使用样式表来自定义控件的外观及其行为的某些方面。在控件上设置样式表的功能是在 Qt 4.2 中引入的，我们将在本章中通过一个简单的示例来领略其可能性。

![](img/9bfe0a027fcc8793bb087287001100dd_335_0.png)

有时，我们不仅仅需要自定义特定的控件，而是需要创建一个结合了两个或更多其他控件的复合控件。我们将查看一个简单的示例，说明如何做到这一点。

如果需要改变现有控件的行为，使其超出仅通过设置属性所能达到的范围，我们可以对该控件进行子类化，并重新实现必要的任何事件处理器，以实现我们要控制的程度。

但在某些情况下，我们需要一个与任何标准内置控件都不同的控件。对于这些情况，我们可以直接对 `QWidget` 进行子类化，并完全由我们自己定义控件的行为和外观。我们将展示这两个方面的示例，第一个是一个可能在许多地方和许多应用程序中使用的“通用”控件，第二个是为单个程序创建的特定于应用程序的控件。

## 使用控件样式表

我们已经看到了许多通过更改属性来自定义控件的示例。其中一些影响了控件的行为，例如设置 `QSpinBox` 的范围，而另一些则影响了控件的外观，例如设置 `QLabel` 的边框。Qt 4.2 引入了一个新的控件属性，即样式表属性。此属性保存一个 `QString`，并使用从 HTML5 CSS（层叠样式表）借来的语法。

图 11.1 中的截图显示了一个设置了样式表的对话框。样式表应用于其所在的控件以及该控件的所有子控件。在这种情况下，我们设置了组合框使用深蓝色文本，行编辑框使用深绿色文本。我们还设置了“强制”的行编辑框具有黄色背景。

![](img/9bfe0a027fcc8793bb087287001100dd_336_0.png)

PyQt 控件没有“mandatory”属性，但从 Qt 4.2 开始，可以动态地将属性添加到 `QObjects`。请注意，Qt 属性与 Python 属性不同——例如，它们使用 `property()` 和 `setProperty()` 进行访问。从 PyQt 4.2 开始，可以使用 `QtCore.pyqtProperty()` 函数来创建既是 Python 属性又是 Qt 属性的属性。

```python
self.lineEdits = (self.forenameEdit, self.surnameEdit,
                  self.companyEdit, self.phoneEdit,
                  self.emailEdit)

for lineEdit in self.lineEdits:
    lineEdit.setProperty("mandatory", QVariant(True))
```

> *样式表在 Mac OS X 上未得到官方支持，因此其行为可能不可预测。预计从 Qt 4.4 开始将得到支持。

```python
self.connect(lineEdit, SIGNAL("textEdited(QString)"),
            self.updateUi)
```

前面的代码来自表单的初始化程序。它为那些我们不希望用户留空的行编辑框添加了“mandatory”属性。所有 Qt 属性都作为 `QVariants` 保存。信号-槽连接稍后讨论。

我们将控件的样式表创建为类静态变量，并在构造函数末尾将其设置在表单上。我们同样可以轻松地从文件（因为它只是纯文本）或 PyQt 资源中读取样式表。

```python
StyleSheet = """
    QComboBox { color: darkblue; }
    QLineEdit { color: darkgreen; }
    QLineEdit[mandatory="true"] {
        background-color: rgb(255, 255, 127);
        color: darkblue;
    }
"""
...
self.setStyleSheet(ContactDlg.StyleSheet)
```

样式表语法基本上由“选择器”和 属性名: 值 对组成。在上面的片段中，第一行的选择器是 `QComboBox`，这意味着其属性值将应用于作为设置了该样式表的控件之子的任何 `QComboBox` 或 `QComboBox` 子类。在这种情况下，效果是将文本颜色设置为深蓝色。第二个选择器是 `QLineEdit`，其工作原理类似。

第三个选择器更具体：它指定了一个类，以及该类中必须匹配状态的属性。换句话说，这个第三个选择器仅应用于具有“mandatory”属性的 `QLineEdit` 和 `QLineEdit` 子类，且该属性的值为 True。对于这些情况，背景颜色被设置为黄色（指定为 RGB 三元组），文本颜色被设置为深蓝色。

这个对话框比乍一看更为微妙。这是因为只有在类别组合框设置为“Business”时，公司行编辑框才是强制的。为了实现这一点，我们需要之前显示的信号-槽连接，以及另一个连接：

```python
self.connect(self.f.categoryComboBox, SIGNAL("activated(int)"),
            self.updateUi)
```

所有连接都指向 `updateUi()` 方法：

```python
def updateUI(self):  
    mandatory = self.companyEdit.property("mandatory").toBool()  
    if self.categoryComboBox.currentText() == "Business":  
        if not mandatory:  
            self.companyEdit.setProperty("mandatory",  
                QVariant(True))  
        
    elif mandatory:  
        self.companyEdit.setProperty("mandatory", QVariant(False))  
        
    if mandatory != self.companyEdit.property("mandatory").toBool():  
        self.setStyleSheet(ContactDlg.StyleSheet)  
        
    enable = True  
    for lineEdit in self.lineEdits:  
        if lineEdit.property("mandatory").toBool() and \  
            lineEdit.text().isEmpty():  
            enable = False  
            break  

    self.buttonBox.button(QDialogButtonBox.Ok).setEnabled(enable)
```

如果用户更改了类别，我们必须重新应用样式表以强制控件重新应用样式。这确保了公司行编辑框的背景根据是否为强制项而正确设置为白色或黄色。不幸的是，在较慢的机器上，重置样式表时会有轻微闪烁——出于这个原因，我们有略微冗长的代码，以确保仅在必要时重新应用样式表。对于“伪状态”（如 enabled、checked 和 hover）的更改，不需要重新应用样式表。

样式表具有比这个简单示例所暗示的更丰富的语法，且更强大。例如，如果我们处理带有句点的选择器，如 `.QLineEdit`，该选择器仅应用于指定的类，而不应用于其子类。如果我们希望选择器应用于某个特定控件，我们可以对该控件调用 `setObjectName()`，然后使用该名称作为选择器的一部分。例如，如果我们有一个对象名称为“findButton”的按钮，那么仅应用于该按钮的选择器将是 `QPushButton#findButton`。
