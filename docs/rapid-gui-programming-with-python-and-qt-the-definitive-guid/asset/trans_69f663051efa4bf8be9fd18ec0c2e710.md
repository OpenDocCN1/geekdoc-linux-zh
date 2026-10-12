
由于 HTML 相当冗余，计算中使用的字符数量可能远大于实际显示的字符数量。

解决此问题有两种方案，两者都需要我们自己计算 HTML 文本的尺寸提示。一种方案是修改 `QAbstractTableModel.data()` 方法，并在以 `Qt.SizeHintRole` 调用 `data()` 时返回合适的尺寸提示。另一种方案是重新实现 `QItemDelegate.sizeHint()` 方法。我们更倾向于重新实现 `sizeHint()`，因为这样可以将问题及其解决方案保留在同一个类中。

```python
def sizeHint(self, option, index):
    fm = option.fontMetrics
    if index.column() == TEU:
        return QSize(fm.width('9,999,999'), fm.height())
    if index.column() == DESCRIPTION:
        text = index.model().data(index).toString()
        document = QTextDocument()
        document.setDefaultFont(option.font)
        document.setHtml(text)
        return QSize(document.idealWidth() + 5, fm.height())
    return QItemDelegate.sizeHint(self, option, index)
```

`option` 参数是一个 `QStyleOptionViewItem`，它是 `QStyleOption` 的一个子类，具有几个有用的属性。在此方法中，我们实际上承担了两个列的尺寸提示职责。对于 TEU 列，我们返回一个足够宽的尺寸提示，以容纳我们预期处理的最大 TEU 值。对于描述列，我们使用 `QTextDocument()` 根据字体和字体属性计算文本的“理想”宽度，并加上 5 像素的小边距。对于其他列，我们将工作移交给基类。

通常，委托（delegate）根本不会重新实现 `paint()` 方法，而是依赖绘制默认行为（这已经足够好），仅提供用于编辑数据项的自定义方法。

```python
def createEditor(self, parent, option, index):
    if index.column() == TEU:
        spinbox = QSpinBox(parent)
        spinbox.setRange(0, 200000)
        spinbox.setSingleStep(1000)
        spinbox.setAlignment(Qt.AlignRight|Qt.AlignVCenter)
        return spinbox
    elif index.column() == OWNER:
        combobox = QComboBox(parent)
        combobox.addItems(sorted(index.model().owners()))
        combobox.setEditable(True)
        return combobox
    elif index.column() == COUNTRY:
        combobox = QComboBox(parent)
        combobox.addItems(sorted(index.model().countries()))
        combobox.setEditable(True)
        return combobox
    elif index.column() == NAME:
        editor = QLineEdit(parent)
        self.connect(editor, SIGNAL("returnPressed()"),
                  self.commitAndCloseEditor)
        return editor
    elif index.column() == DESCRIPTION:
        editor = richtextlineedit.RichTextLineEdit(parent)
        self.connect(editor, SIGNAL("returnPressed()"),
                  self.commitAndCloseEditor)
        return editor
    else:
        return QItemDelegate.createEditor(self, parent, option,
                                      index)
```

当用户发起对某个数据项的编辑时（通常通过按 F2 或双击实现），视图会要求委托为该数据项提供编辑器。对于我们不想或不需要自行处理的项，我们可以简单地将工作移交给基类，但在此委托中，我们更喜欢自己处理每一列。

对于 TEU 列，我们创建并返回一个数字输入框（spinbox）。我们可以使用任何小部件，无论是内置的如 `QSpinBox`，还是自定义编辑器，例如我们在前一章创建的 `RichTextLineEdit`。在所有情况下，步骤都是相同的：使用给定的父对象创建编辑器，然后设置并返回它。

我们在组合框中填入了排序后的列表，并使其可编辑，以便用户可以添加新条目。如果我们希望用户只能从我们指定的列表中选择，我们只需省略 `setEditable(True)` 调用即可。

在 `QLineEdit`、`QTextEdit` 以及其他具有 `returnPressed()` 信号（指示编辑已完成）的类中，我们将该信号连接到 `commitAndCloseEditor()` 方法的重新实现。

```python
def commitAndCloseEditor(self):
    editor = self.sender()
    if isinstance(editor, (QTextEdit, QLineEdit)):
        self.emit(SIGNAL("commitData(QWidget*)"), editor)
        self.emit(SIGNAL("closeEditor(QWidget*)"), editor)
```

以前，我们始终使用内置的 `instance()` 函数来根据单个类考虑对象，但在这里我们提供了两个类的元组。当用户按下回车键时调用此方法，进而发出信号通知编辑器将其数据保存到模型并关闭自身。

![](img/9bfe0a027fcc8793bb087287001100dd_454_0.png)

```python
def setEditorData(self, editor, index):
    text = index.model().data(index, Qt.DisplayRole).toString()
    if index.column() == TEU:
        value = text.replace(QRegExp("[, ]+"), "").toInt()[0]
        editor.setValue(value)
    elif index.column() in (OWNER, COUNTRY):
        i = editor.findText(text)
        if i == -1:
            i = 0
        editor.setCurrentIndex(i)
    elif index.column() == NAME:
        editor.setText(text)
    elif index.column() == DESCRIPTION:
        editor.setHtml(text)
    else:
        QItemDelegate.setEditorData(self, editor, index)
```

一旦编辑器被创建并交给视图，视图就会调用 `setEditorData()`。这给了委托一个机会，用当前数据填充编辑器，以便用户进行编辑。对于 TEU，我们以文本形式显示它们，可能包含空格、逗号或句点。因此，对于这些项，我们去掉不需要的字符，将值转换为整数，并相应地设置数字输入框的值。另一种方法是为该列使用单独的 `Qt.DisplayRole` 和 `Qt.EditRole` 值。

如果编辑器是一个组合框，我们将当前索引设置为与数据值匹配的项目。如果没有匹配项，我们就简单地使第一个项目成为当前项。对于用于船舶名称的行编辑框，我们使用 `setText()`；对于富文本行编辑框，我们使用 `setHtml()`（继承自 `QTextEdit`）。一如既往，我们将未处理的情况移交给基类，尽管在这里这只是一个形式，因为我们自己处理了所有列。

```python
def setModelData(self, editor, model, index):
    if index.column() == TEU:
        model.setData(index, QVariant(editor.value()))
    elif index.column() in (OWNER, COUNTRY):
        model.setData(index, QVariant(editor.currentText()))
    elif index.column() == NAME:
        model.setData(index, QVariant(editor.text()))
    elif index.column() == DESCRIPTION:
        model.setData(index, QVariant(editor.toSimpleHtml()))
    else:
        QItemDelegate.setModelData(self, editor, model, index)
```

如果用户确认其编辑，编辑器的数据必须写回模型。然后，模型将通知视图该项已更改，而显示该项的视图将请求新的数据以进行显示。

在每种情况下，我们只需从相应的编辑器中检索值并调用 `setData()`，将值作为 `QVariant` 传递。

我们现在已完成委托。下一章将使用两个委托，它们都为某些字段提供编辑器，并且都仅实现 `createEditor()`、`setEditorData()` 和 `setData()`。在本章和下一章中，自定义委托是针对特定模型的。但在第 16 章中，我们有一个专门用于“通用委托”的章节，它可以用于为任何模型创建委托，而无需拥有模型特定的自定义委托——这可以减少代码重复并使维护更容易。

## 摘要

PyQt 的便捷项视图小部件，如 `QListView`、`QTableView` 和 `QTreeView`，对于查看和编辑小型及临时数据集非常有用。我们可以像第一部分那样将它们与外部数据库结合使用，或者将它们本身用作数据容器。添加、编辑和删除项都很简单，但如果我们使用多个视图来显示一个数据集，我们必须接受保持视图和数据集同步的责任。如果我们使用带有自定义模型的模型/视图方法，这个问题就会消失。

便捷视图没有提供对其所处理项编辑的任何控制。通过设置我们自己的自定义项委托，可以轻松修正这一缺陷，无论是对于便捷视图还是纯视图。

纯视图提供与便捷视图类似的功能，但不提供排序或对数据项外观的直接控制。必须将这些视图与模型结合使用，无论是 PyQt 提供的预定义模型，还是更常见的我们自己的自定义模型。

要实现自定义表格模型，我们必须为只读和可编辑模型重新实现 `rowCount()`、`columnCount()` 和 `data()`；通常还必须重新实现 `headerData()`。此外，我们必须实现 `flags()` 和 `setData()` 以使项可编辑，并实现 `insertRows()` 和 `removeRows()` 以允许用户插入或删除数据行。如果我们希望用户能够排序数据，我们可以添加额外的排序方法，尽管对于数据库表，我们只需添加 `ORDER BY` 子句即可。使用数据库配合模型/视图架构的内容将在下一章中介绍。

创建自定义委托使我们能够完全控制数据项的外观和编辑。模型和委托之间可以分担数据外观的责任，或者将所有责任交给其中一方。但只有自定义委托可用于提供编辑控制。对于只读委托，以及仅关注数据外观的委托，我们通常只需要重新实现 `paint()` 方法，尽管在某些情况下，我们还必须重新实现 `sizeHint()`（或在模型的 `data()` 中处理 `Qt.SizeHintRole`）。

