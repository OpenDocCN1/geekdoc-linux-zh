
与前一节的唯一区别是，我们调用了 `setItemDelegate()`，并传入一个新构建的 `ship.ShipDelegate`。必须将表单作为委托的父级，以便在表单使用期间保持委托的活跃状态。第二个表格的代码是一样的，设置相同的模型，但拥有自己的 `ship.ShipDelegate`。这是唯一必要的更改——现在所有呈现和编辑数据的工作都将由委托处理。

```python
class ShipDelegate(QItemDelegate):
    def __init__(self, parent=None):
        super(ShipDelegate, self).__init__(parent)
```

通常情况下，除了初始化基类之外，委托的构造函数不需要做任何其他事情，这里我们只做了这一点。事实上，对于这种情况，我们可以完全省略 `__init__()`。

```python
def paint(self, painter, option, index):
    if index.column() == DESCRIPTION:
        txt = index.model().data(index).toString()
        palette = QApplication.palette()
        document = QTextDocument()
        document.setDefaultFont(option.font)
        if option.state & QStyle.State_Selected:
            document.setHtml(QString("<font color=%2s/>").arg(palette.highlightedText().color().name()) \
                    .arg(txt))
        else:
            document.setHtml(txt)
        color = palette.highlight().color() \
        if option.state & QStyle.State_Selected \
        else QColor(index.model().data(index,
        Qt.BackgroundColorRole)
  painter.save()
  painter.fillRect(option.rect, color)
  painter.translate(option.rect.x(), option.rect.y())
  document.drawContents(painter)
  painter.restore()
else:
  QItemDelegate.paint(self, painter, option, index)
```

对于纯文本字符串、数字、日期等，基类 `QItemDelegate.paint()` 方法工作得非常好，因此很常见的是根本不重新实现它。然而，在这个例子中，描述列包含 HTML，这必须由我们自己渲染。

`paint()` 方法被调用时，画笔已准备好进行绘制，还有一个 `QStyleOptionViewItem`，它包含各种信息，包括绘制应发生的矩形区域，以及要绘制的项的模型索引。

我们首先使用模型的 `data()` 方法获取 HTML 文本，并依赖我们在模型中为第二个参数设置的 `Qt.DisplayRole` 默认值。请注意，模型索引可以通过 `QModelIndex.model()` 方法为我们提供其所引用的模型的引用。

然后，我们获取应用程序的调色板——这是基于用户的主题颜色偏好。如果该项被选中，我们将调色板的高亮文本颜色应用于 HTML；否则，我们“原样”使用 HTML。`QColor.name()` 方法以十六进制字符串的形式返回颜色；例如，红色将被返回为字符串 “#FF0000”，这与 HTML 颜色规范使用的格式相同。同样，如果该项被选中，我们使用调色板的高亮背景颜色；否则，我们使用通过调用 `data()` 方法并传入 `Qt.BackgroundColorRole` 而由模型指定的背景颜色。

`QTextDocument.drawContents()` 方法相对于画笔的左上角 `(0, 0)` 坐标进行绘制。因此，我们将画笔的左上角移动（平移）到样式选项矩形的 `(x, y)` 位置，然后告诉文档在画笔上绘制自身。

在许多情况下，我们不必在绘制事件之间费心保存和恢复画笔的状态，但在这种情况下我们必须这样做。一些 Qt 程序员认为始终保存和恢复画笔的状态是一种好的做法，而另一些人则倾向于仅在必要时这样做，即仅当我们对画笔状态应用持久更改时，例如应用变换（如平移）。

不幸的是，绘制 HTML 的故事并没有就此结束。当视图请求 HTML 列的大小提示时，默认行为将是基于视图的字体和字符数返回大小提示。

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

`option` 参数是一个 `QStyleOptionViewItem`，它是 `QStyleOption` 的一个子类，具有几个有用的属性。在此方法中，我们实际上承担了两个列的尺寸提示职责。对于 `TEU` 列，我们返回一个足够宽的尺寸提示，以容纳我们预期处理的最大 TEU 值。对于描述列，我们使用 `QTextDocument()` 根据字体和字体属性计算文本的“理想”宽度，并加上 5 像素的小边距。对于其他列，我们将工作移交给基类。

通常，委托（delegate）根本不会重新实现 `paint()` 方法，而是依赖绘制默认行为（这已经足够好），仅提供用于编辑数据项的自定义方法。
