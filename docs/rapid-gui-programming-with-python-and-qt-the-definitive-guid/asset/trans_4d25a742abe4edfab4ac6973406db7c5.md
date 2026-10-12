

## 跨列验证

`IntegerColumnDelegate` 和 `DateColumnDelegate` 的子类被用于提供跨列验证。例如，我们不接受返回日期早于雇佣日期的情况，或者不接受里程数小于起始里程数的情况。

```python
class HireDateColumnDelegate(genericdelegates.DateColumnDelegate):
    def createEditor(self, parent, option, index):
        i = index.sibling(index.row(), RETURNED)
        self.maximum = i.model().data(i, Qt.DisplayRole).toDate().addDays(-1)
        return genericdelegates.DateColumnDelegate.createEditor(self, parent, option, index)
```

这是完整的 `HireDateColumnDelegate` 子类。我们只需要重新实现 `createEditor()` 方法。我们获取返回日期，并将最大雇佣日期设置为车辆返回日期的前一天，因为我们至少租用一天。我们实际上将编辑器的创建留给基类。我们无法在创建列委托时设置一个有意义的最大日期，因为用户可能随时编辑返回日期，因此我们必须在使用者开始编辑时计算最大雇佣日期。

使用 `sibling()` 方法提供了比调用 `index.model().index(index.row(), RETURNED)` 更方便的替代方案。

`ReturnDateColumnDelegate` 几乎相同，只是我们获取雇佣日期，并将最小返回日期设置为车辆雇佣日期的次日。`MileageOutColumnDelegate` 和 `MileageBackColumnDelegate` 类似；它们都只重新实现了 `createEditor()` 方法，并且都根据另一个里程数的值设置最大值（或最小值）。

模型的 `setData()` 方法不允许编辑许可证号或生成的列。它通过简单地为这些列返回 `False` 来实现，这表明它们未被更新。对于其他列，传递给 `setData()` 方法的值会设置到底层数据结构中。

模型的 `data()` 方法忠实地返回其被要求提供的列的值，这些值由底层数据结构提供。数据结构为大多数列返回存储的值，但对于 `MILEAGE` 和 `DAYS` 列，它返回根据相关值计算出的结果。

创建通用的数据类型特定的列委托非常容易，而在验证必须考虑整行（记录）时对其进行子类化也不难。但是，既然为每个模型创建自定义委托并不困难，为什么要使用通用委托方法呢？主要有两种情况下通用委托没有意义：只需要少数委托的简单应用程序，以及包含异构数据类型的列的模型。但对于需要许多委托且列具有同质数据类型（如数据库中使用的类型）的应用程序，通用委托提供了三个关键优势：

- 更改用于特定列的委托，或者如果模型更改为拥有更多列时添加额外的列委托，都很容易。
- 使用列委托意味着我们避免了如果创建许多模型特定的自定义委托时不可避免的代码重复——例如，我们只需要编写一个富文本行编辑委托，一个日期/时间编辑委托等。
- 一旦创建了数据类型特定的列委托，它可以用于任何使用该数据类型的每一列，在任何数量用于任何数量模型的通用委托中重用。这意味着针对每种数据类型的错误修复和改进只需应用于一个列委托。

### 在树中表示表格数据

假设我们希望用户选择某个数据项，但他们选择的项目依赖于他们之前选择的某个项目，而这又依赖于更早前的某个项目。具体来说，想象我们要用户选择一个特定的机场——首先他们必须选择国家，然后是城市，然后是机场。这可以通过提供三个组合框来实现，第一个填充国家名称，第二个填充当前国家的城市，第三个填充当前城市的机场。编程这并不难，但用户必须看到三个独立的小部件来指定他们的选择，并且无法轻松看到有哪些可供选择的范围。

选择依赖数据项的一个解决方案是使用树视图。继续这个例子，树的根将是国家，每个国家将有城市分支，每个城市分支将有机场叶子。这使得用户更容易遵循路径（并且他们只能遵循有效路径），也更容易让我们检索他们完整的国家/城市/机场选择。

使用树视图的另一个好处（例如与使用表格视图相比）是它更紧凑且更容易导航。例如，如果我们拥有 100 个国家，平均每个国家 4 个城市，每个城市平均 2 个机场，表格将需要 100 × 4 × 2 = 800 行——但树只需要 100 行（每个国家一行），每行都可以展开显示其城市和机场。

在本节中，我们将展示如何在树中表示数据表格，以及如何提取用户选择的完整“路径”。我们将使用的应用程序示例称为 Server Info。它读取一个具有六列的数据集——国家、州（仅对美国有意义）、城市、提供商、服务器和 IP 地址——并允许用户指定一个特定的 6 元组。示例数据集有 163 行，但仅引用 33 个独特的国家，因此用户只需导航 33 个顶级项，而不是滚动浏览几乎五倍于此数量的行。

![](img/9bfe0a027fcc8793bb087287001100dd_507_0.png)

**图 16.3 以树形式呈现的表格数据**

应用程序的核心由 `TreeOfTableModel` 类提供，这是一个 `QAbstractItemModel` 子类，可以在树中表示任意的表格数据。我们使用该模型的一个自定义子类，以及一个 `QTreeView` 子类来展示数据。应用程序本身可以通过在控制台运行时使用 1、2、3 或 4 作为命令行参数来创建具有不同嵌套层级的树。图 16.3 显示了使用默认嵌套级别 3 的树。（嵌套级别不包括一系列分支末端的叶子。）

我们将首先回顾主表单，因为它非常简短。然后我们将查看表格视图子类和 `TreeOfTableModel` 子类。接下来，我们将回顾 `treeoftable` 模块，包括 `BranchNode` 和 `LeafNode` 类，最后是 `TreeOfTableModel` 类本身。

```python
class MainForm(QMainWindow):
    def __init__(self, filename, nesting, separator, parent=None):
        super(MainForm, self).__init__(parent)
        headers = ["Country/State (US)/City/Provider", "Server", "IP"]
        self.treeWidget = TreeOfTableWidget(filename, nesting, separator)
        self.treeWidget.model().headers = headers
        self.setCentralWidget(self.treeWidget)
        self.connect(self.treeWidget, SIGNAL("activated"), self.activated)
        self.setWindowTitle("Server Info")
```

`TreeOfTableWidget` 类似于便利视图，因为它内部包含了一个模型。该模型是 `ServerModel`，一个小的 `TreeOfTableModel` 子类，增加了显示旗帜图标的功能。

`filename` 是具有适合 `TreeOfTableModel` 数据的文件名称。特别是，它必须每行一条记录，并且每个列（字段）必须由指定的分隔符分隔。

`nesting` 值是可以从根节点分出的最大分支数，不包括末端的叶子。在这种情况下，通过 `nesting` 参数传入的嵌套值为 3（除非在命令行上更改），这意味着我们将有 3 层分支（国家、州、城市）和 1 层叶子（提供商）。由于我们有 6 个字段，这意味着前 4 个字段将显示在树小部件的树部分，剩余的 2 个字段将作为单独的列显示在具有叶子的行中。结果树视图将有 3 列，一列包含树，另外 2 列显示额外字段。我们通过直接访问自定义 `TreeOfTableWidget` 内部的模型来设置模型的头。

`activated()` 方法在用户双击树小部件中的某一行或按 Enter 键时调用。

```python
def activated(self, fields):
    self.statusBar().showMessage("+".join(fields), 60000)
```

“路径”，即用户选择的（国家，城市，州，提供商，服务器，IP 地址）6 元组，每当合适的行被激活时，都会在状态栏中以“+”分隔显示一分钟（60,000 毫秒）。在此上下文中，合适的行是包含叶子的行，因为这些是唯一拥有全部六个字段的行。

`TreeOfTableWidget` 是一个包含其显示模型的 `QTreeView` 子类。它还提供了几个简单的便利方法，并创建了一些有用的信号—槽连接。

```python
class TreeOfTableWidget(QTreeView):
    def __init__(self, filename, nesting, separator, parent=None):
        super(TreeOfTableWidget, self).__init__(parent)
        self.setSelectionBehavior(QTreeView.SelectItems)
        self.setUniformRowHeights(True)
        model = ServerModel(self)
        self.setModel(model)
        try:
            model.load(filename, nesting, separator)
        except IOError, e:
            QMessageBox.warning(self, "Server Info - Error", unicode(e))
        self.connect(self, SIGNAL("activated(QModelIndex)"), self.activated)
```

