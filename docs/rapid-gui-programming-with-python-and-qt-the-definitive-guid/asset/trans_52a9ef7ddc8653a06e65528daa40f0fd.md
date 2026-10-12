

## 1. 文本重构与OCR纠正说明
（注：根据指令，此处仅展示最终处理后的文本，无额外解释。）

## 创建对话框并传入格式字典
我们首先创建对话框，并将从对话框初始化所使用的格式字典以及 `self` 传递给它，从而使对话框与调用表单绑定——居中于其上，并且不拥有自己的任务栏条目。

正如我们之前提到的，调用 `exec()` 会弹出对话框，因此它是作为模态对话框调用的，这意味着用户在与其父窗口及其兄弟窗口交互之前，必须接受或拒绝该对话框。在下一节中，我们将使用没有此限制的对话框模式版本。

如果用户点击“确定”，我们将格式字典设置为对话框中设定的值，并更新表格，以便使用新格式显示数字。如果用户取消，我们不做任何操作。在方法结束时，对话框超出作用域范围，因此将被安排进行垃圾回收。

为了节省空间并避免不必要的重复，从现在开始，除非其存在并不明显，否则我们不再展示任何导入语句。因此，例如，我们不再显示 `from PyQt4.QCore import *` 或 `from PyQt4.QtGui import *`。

现在，我们准备查看对话框本身的实现。

```python
class NumberFormatDlg(QDialog):
    def __init__(self, format, parent=None):
        super(NumberFormatDlg, self).__init__(parent)
```

`__init__()` 方法与我们之前看到的其他所有对话框的开始方式相同。

```python
        thousandsLabel = QLabel("&Thousands separator")
        self.thousandsEdit = QLineEdit(format["thousandsseparator"])
        thousandsLabel.setBuddy(self.thousandsEdit)
        decimalMarkerLabel = QLabel("Decimal &marker")
        self.decimalMarkerEdit = QLineEdit(format["decimalmarker"])
        decimalMarkerLabel.setBuddy(self.decimalMarkerEdit)
        decimalPlacesLabel = QLabel("&Decimal places")
        self.decimalPlacesSpinBox = QSpinBox()
        decimalPlacesLabel.setBuddy(self.decimalPlacesSpinBox)
        self.decimalPlacesSpinBox.setRange(0, 6)
        self.decimalPlacesSpinBox.setValue(format["decimalplaces"])
        self.redNegativesCheckBox = QCheckBox("&Red negative numbers")
        self.redNegativesCheckBox.setChecked(format["rednegatives"])

        buttonBox = QDialogButtonBox(QDialogButtonBox.Ok |
                                      QDialogButtonBox.Cancel)
```

对于我们希望用户能够修改的格式的每个方面，我们创建一个标签让用户知道他们正在编辑什么，以及一个合适的编辑控件。由于 `format` 参数是强制性的，我们假设它拥有我们需要的所有值，因此我们使用它来初始化编辑控件。我们还使用 `setBuddy()` 调用来支持键盘用户，因为并非所有用户都能使用鼠标。

### 表 5.2 QDialogButtonBox 选定的方法和信号

| 语法 | 描述 |
| :--- | :--- |
| `d.addButton(b, r)` | 将带有 `QDialogButtonBox.ButtonRole r` 的 `QPushButton b` 添加到 `QDialogButtonBox d` |
| `d.addButton(t, r)` | 将带有文本 `t` 和按钮角色 `r` 的 `QPushButton` 添加到 `QDialogButtonBox d`，并返回添加的按钮 |
| `d.addButton(s)` | 将指定为 `QDialogButtonBox.StandardButton s` 的 `QPushButton` 添加到 `QDialogButtonBox d`，并返回添加的按钮 |
| `d.setOrientation(o)` | 将 `QDialogButtonBox` 的方向设置为 `Qt.Orientation o`（垂直或水平） |
| `d.button(s)` | 返回指定为 `StandardButton s` 的 `QDialogButtonBox` 的 `QPushButton`，如果不存在则返回 `None` |
| `d.accepted()` | 如果带有 `QDialogButtonBox.Accept` 角色的按钮被点击，则发出此信号 |
| `d.rejected()` | 如果带有 `QDialogButtonBox.Reject` 角色的按钮被点击，则发出此信号 |

我们实施的唯一验证是限制小数位数自旋框的范围。我们选择了“事后”验证方法，即在用户输入值之后，在用户点击“确定”接受编辑的时刻进行验证。在下一节中，我们将看到“预防性”验证，这种方法从源头上防止无效编辑。

```python
self.format = format.copy()
```

我们需要对传入的格式字典进行*复制*，因为我们希望能够在对话框内部修改该字典而不影响原始字典。

```python
grid = QGridLayout()
grid.addWidget(thousandsLabel, 0, 0)
grid.addWidget(self.thousandsEdit, 0, 1)
grid.addWidget(decimalMarkerLabel, 1, 0)
grid.addWidget(self.decimalMarkerEdit, 1, 1)
grid.addWidget(decimalPlacesLabel, 2, 0)
grid.addWidget(self.decimalPlacesSpinBox, 2, 1)
grid.addWidget(self.redNegativesCheckBox, 3, 0, 1, 2)
grid.addWidget(buttonBox, 4, 0, 1, 2)
self.setLayout(grid)
```

布局的外观与我们在画笔属性对话框中使用的布局非常相似，只是这次我们有一个 `QDialogButtonBox` 控件，而不是用于按钮的布局。这使得使用单个 `QGridLayout` 创建整个布局成为可能。

![](img/9bfe0a027fcc8793bb087287001100dd_165_0.png)

“红色负数”复选框和按钮框的布局都设置为各占据一行和两列。行跨度和列跨度由 `QGridLayout` 的 `addWidget()` 和 `addLayout()` 方法的最后两个参数指定。布局如图 5.4 所示，网格以阴影显示。

```python
self.connect(buttonBox, SIGNAL("accepted()"),
             self, SLOT("accept()"))
self.connect(buttonBox, SIGNAL("rejected()"),
             self, SLOT("reject()"))
self.setWindowTitle("Set Number Format (Modal)")
```

建立连接和设置窗口标题的代码与我们在画笔属性对话框中使用的类似，只是这次我们使用按钮框的信号，而不是直接连接到按钮本身。

```python
def numberFormat(self):
    return self.format
```

如果用户点击“确定”，对话框被接受并返回 True 值。在这种情况下，调用表单的方法通过调用 `numberFormat()` 方法，用对话框的字典覆盖其格式字典。由于我们没有将对话框的 `self.format` 属性变得非常私有（即通过将其命名为 `__format__`），我们可以从表单外部直接访问它；我们将在后续示例中采用这种方法。

当用户点击“确定”时，由于我们使用的是事后验证，因此可能存在某些编辑控件包含无效数据的情况。为了处理这个问题，我们重新实现 `QDialog.accept()`，并在其中进行验证。由于该方法相当长，我们将分部分查看它。

```python
def accept(self):
    class ThousandsError(Exception): pass
    class DecimalError(Exception): pass
    Punctuation = frozenset(" ,;;.")
```

我们首先创建两个异常类，我们将在 `accept()` 方法内部使用它们。这将有助于使我们的代码比否则可能的更干净、更简短。我们还创建了一个字符集，允许这些字符用作千位分隔符和小数点标记。

我们唯一担心需要验证的编辑控件是两个行编辑框。这是因为小数位数自旋框已经限制在有效范围内，并且“红色负数”复选框只能被选中或取消选中，这两种状态都是有效的。

```python
                thousands = unicode(self.thousandsEdit.text())
                decimal = unicode(self.decimalMarkerEdit.text())
            try:
                if len(decimal) == 0:
                    raise DecimalError, ("The decimal marker may not be "
                        "empty.")

                if len(thousands) > 1:
                    raise ThousandsError, ("The thousands separator may "
                        "only be empty or one character.")

                if len(decimal) > 1:
                    raise DecimalError, ("The decimal marker must be "
                        "one character.")

                if thousands == decimal:
                    raise ThousandsError, ("The thousands separator and "
                        "the decimal marker must be different.")

                if thousands and thousands not in Punctuation:
                    raise ThousandsError, ("The thousands separator must "
                        "be a punctuation symbol.")

                if decimal not in Punctuation:
                    raise DecimalError, ("The decimal marker must be a "
                        "punctuation symbol.")

            except ThousandsError, e:
                QMessageBox.warning(self, "Thousands Separator Error",
                    unicode(e))
                self.thousandsEdit.selectAll()
                self.thousandsEdit.setFocus()
                return

            except DecimalError, e:
                QMessageBox.warning(self, "Decimal Marker Error",
                    unicode(e))
                self.decimalMarkerEdit.selectAll()
                self.decimalMarkerEdit.setFocus()
                return
```

我们首先从两个行编辑框获取文本。虽然没有千位分隔符是可以接受的，但必须存在小数标记，因此我们首先检查 `decimalMarkerEdit` 是否至少有一个字符。如果没有，我们抛出带有适当错误文本的自定义 `DecimalError`。如果任何文本长度超过一个字符，或者它们是相同的字符，或者任何文本包含不在我们的 `Punctuation` 集中的字符，我们也抛出异常。*if* 语句在标点方面有所不同，因为千位分隔符允许为空，但小数点标记不允许。

