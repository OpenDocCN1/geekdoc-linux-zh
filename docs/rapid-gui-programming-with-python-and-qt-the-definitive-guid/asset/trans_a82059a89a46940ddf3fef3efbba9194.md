

```python
return θ
return len(node)
```

对于树模型，行数是指特定节点拥有的子节点数量。我们的实现只允许分支节点拥有子节点，因此当在叶节点上调用时，我们总是返回 0。`len()` 函数调用 `Branch-Node._len_()`，该方法返回分支子节点的数量。

```python
def columnCount(self, parent):
    return self.columns
```

列数是非嵌套字段的最大数量。这看起来可能少了一列，但这是正确的，因为第一个非嵌套字段显示在第一个（树）列中。

```python
def data(self, index, role):
    if role == Qt.TextAlignmentRole:
        return QVariant(int(Qt.AlignTop|Qt.AlignLeft))
    if role != Qt.DisplayRole:
        return QVariant()
    node = self.nodeFromIndex(index)
    assert node is not None
    if isinstance(node, BranchNode):
        return QVariant(node.toString()) \
            if index.column() == 0 else QVariant(QString(""))
    return QVariant(node.field(index.column()))
```

如果请求分支节点的显示数据，我们返回第 0 列的节点文本以及其他列的空字符串。对于叶节点，我们返回与请求列对应的字段。

在 Qt 4.2 之前，默认文本对齐工作正常，无需指定，但从 Qt 4.2 开始，我们必须显式地返回一个合理的文本对齐。

```python
def headerData(self, section, orientation, role):
    if orientation == Qt.Horizontal and \
            role == Qt.DisplayRole:
        assert 0 <= section <= len(self.headers)
        return QVariant(self.headers[section])
    return QVariant()
```

树视图只有水平（列）标题。它们没有行标题（例如行号），因为每个分支都有自己的基于 0 的子节点（行）列表，因此行标题没有实际意义。

```python
def index(self, row, column, parent):
    assert self.root
    branch = self.nodeFromIndex(parent)
    assert branch is not None
    return self.createIndex(row, column,
            branch.childAtRow(row))
```

`index()` 方法必须返回具有给定行和列且是给定父项子项的数据项的模型索引。在分支和叶子的树模型中，这意味着我们必须返回父项的第 `row` 个子项的模型索引。

我们首先找到给定父模型索引的分支节点，然后返回一个模型索引，该索引具有给定的行和列，其父项是（分支）节点的第 `row` 个子节点。

```python
def parent(self, child):
    node = self.nodeFromIndex(child)
    if node is None:
        return QModelIndex()
    parent = node.parent
    if parent is None:
        return QModelIndex()
    grandparent = parent.parent
    if grandparent is None:
        return QModelIndex()
    row = grandparent.rowOfChild(parent)
    assert row != -1
    return self.createIndex(row, 0, parent)
```

`parent()` 方法必须返回给定子项的父项的模型索引。在分支和叶子的树模型中，这是子项的祖父项的第 `row` 个子项。

我们首先找到子节点的父节点的父节点（即子项的祖父项）。然后我们返回一个模型索引，该索引具有父节点在祖父项的子节点列表中占据的行号，第 0 列（因为所有父项都是分支，且分支只有第 0 列），以及父项为子项的父节点。

此处展示的 `index()` 和 `parent()` 方法的实现相当微妙。然而，对于采用分支和叶子方法的树模型而言，这些是标准实现，因此其代码在大多数情况下可以直接“原样”复制。

```python
def nodeFromIndex(self, index):
    return index.internalPointer() \
        if index.isValid() else self.root
```

当我们调用 `QAbstractItemModel.createIndex()` 时，第三个参数是对节点的引用。该引用可从模型索引中获取，并由 `internalPointer()` 方法返回。对于任何给定的模型索引，我们返回一个分支或叶节点，或者是分支根节点。

理解树模型比理解表格模型（或列表模型，它们只是单列表格）更具挑战性。然而，在许多情况下，通过构建或改编本节中介绍的代码，可以减轻这些难度。

## 摘要

PyQt 的内置视图控件和图形视图控件结合起来，为可视化数据集提供了相当大的空间。但是，当我们的需求与这些类提供的功能不匹配时，我们始终可以创建自己的自定义视图，并以我们喜欢的方式展示数据。

由于自定义视图可能会显示非常大的数据集的一部分，通常最好优化绘制事件处理器，以仅检索和显示实际可见的数据项。如果需要滚动条，我们可以要求用户在我们的视图类中使用 `QScrollArea`，或者创建一个包含几个 `QScrollBar` 的复合控件，或者创建一个继承自 `QAbstractScrollArea` 的控件。这些方法中的第一种方法只需在用户代码中添加几行，并使实现视图变得更加容易。

使用通用委托配合特定数据类型的列委托，可以轻松创建即时的“自定义”视图委托。列委托很容易创建，并且可以减少代码重复，因为我们只需要为每种想要处理的数据类型创建一个列委托。通用委托方法非常适合每个列的数据只保存单一数据类型值的数据集，例如数据库表。

创建树模型可能很困难，因为我们必须以父项和子项的术语来思考，其中子项也可以是父项，并以此类推递归到任意深度。这并不像树形和列模型所需的行和列术语思考那么简单。虽然本章介绍的表格树模型是一个特定示例，但提供其树形功能的一些方法（如 `index()`、`parent()` 和 `nodeFromIndex()`）应该能够“原样”使用或只需少量改编，而其他方法（如 `addRecord()`）也应该证明是可改编的。

## 练习

本练习综合了本章及前几章中介绍的许多模型/视图特性。

创建一个应用程序，显示两个控件：一个 `QListView` 和一个自定义的 `Bar-GraphView`。数据应保存在自定义的 `BarGraphModel` 中。用户应能通过 `QListView` 编辑数据，并使用自定义的 `BarGraphDelegate` 来控制列表视图中数据项的展示和编辑。

应用程序如图 16.5 所示。

![](img/9bfe0a027fcc8793bb087287001100dd_520_0.png)

模型应该是 `QAbstractListModel` 的子类，它应保存一个数据值列表（整数）和一个颜色字典（以“行”为键；例如，键为 6 的颜色对应于第七个数据值，依此类推）。模型应重新实现 `rowCount()`、`insertRows()`——其中应在适当的地方包含对 `beginInsertRows()` 和 `endInsertRows()` 的调用、`flags()` 以使模型可编辑，以及 `setData()` 以允许设置值（`Qt.DisplayRole`）和值的颜色（`Qt.UserRole`），并且应发出信号以指示数据已更改——以及 `data()`，它应返回值、颜色，以及对于 `Qt.DecorationRole`，一个填充了该颜色的 20 × 20 像素图。如果未为特定行设置颜色，则使用红色作为默认值。

委托非常简单，并且与本章前面提到的 `IntegerColumnDelegate` 非常相似。关键区别在于必须重新实现 `paint()` 方法，但只是为了将对齐设置为 `Qt.AlignRight`；绘制仍然可以由基类很好地完成。

自定义视图需要重新实现 `setModel()`，其中应建立与基类的 `update()` 方法的连接，以便在模型数据更改时发生重绘；`minimumSizeHint()`、`sizeHint()`——它可以直接调用 `minimumSizeHint()`——以及 `paintEvent()`。绘制事件可以用略多于一两行代码完成——请确保使用 `QPainter.setWindow()`，以便图形始终填满可用空间。如果没有设置模型，所有方法都应正确工作——例如，在没有模型的情况下，绘制事件不应绘制任何内容。

以下是 MainForm 的代码，供你感受这些类是如何使用的：

```python
class MainForm(QDialog):

    def __init__(self, parent=None):
```

