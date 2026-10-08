

# 教程

![](img/c7d3278283754436651c50a2e9c72912_43_0.png)

上述过滤器可用于限制显示的信息量。

```cpp
void MainWindow::itemDoubleClicked(QModelIndex _anIndex)
{
  QFileSystemModel* whatModel = ((QFileSystemModel*) ui->treeView->model());
  QFileInfo myFile = whatModel->fileInfo(_anIndex);
  QMessageBox *aBox=new QMessageBox();
  aBox->setText(myFile.path());
  aBox->show();
}
```

```cpp
#include <QSortFilterProxyModel>

class ImagineFilterModel:public QSortFilterProxyModel
{
  Q_OBJECT
 public:
  ImagineFilterModel(QObject *parent);
};
```

```cpp
#include "imagefiltermodel.h"

ImagineFilterModel::ImagineFilterModel(QObject *parent):
 QSortFilterProxyModel(parent)
{
 QFileSystemModel* myModel1=new QFileSystemModel(this);
 myModel1->setRootPath("/");
 setSourceModel(myModel1);
}
```

```cpp
MainWindow::MainWindow(QWidget *parent) :
 QMainWindow(parent),
 ui(new Ui::MainWindow)
{
 ui->setupUi(this);
 ImagineFilterModel* myModel=new ImagineFilterModel(this);
 ui->treeView->setModel(myModel);
}
```

连接对话框是建立连接的地方。我们已在几期之前的文章中详细介绍了这一过程，但你也可以通过简单的网络搜索找到有关打开对话框的更多信息。

虽然 Qt 会自动为我们创建信号和插槽之间的连接，但我们必须手动实现相应的方法。打开 `mainform.h` 并将**图 03** 中的声明添加到该类中。

项目视图发出的信号包含一个 `QModelIndex`。这是一个方便的条目，提供有关待处理元素的进一步信息。我们可以使用此值来了解有关当前文件的更多信息（**图 04**）。

我们的表单构造函数没有将模型指针存储在 global 变量中。我们首先调用 `model()` 方法，该方法返回指向 `QAbstractModel` 的指针。`QFileSystemModel` 的结构使得模型不能包含除 `QFileSystemModel` 以外的任何内容，因此我们只需将返回值强制转换为其期望的类型。

在下一步中，查询实例以了解有关相关项目的更多细节。然后，这些信息在 `QMessageBox` 中显示。

# 模型无限多

使用 `QFileSystemModel` 让我们能够以最小的努力创建文件和文件夹查看器。我们仅使用了该类的少量功能；它可以过滤文件夹并执行各种其他令人印象深刻的功能。

希望从 Qt 中获取价值的开发者会很高兴地听到，该框架包含半打不同的模型，专门用于各种有用的任务。例如，通过使用 `QSqlQueryModel`、`QSqlTableModel` 和 `QSqlRelationalTableModel` 中的一个或全部，可以“封装”数据库访问。

字符串列表应打包到 `QStringListModel` 的实例中。它处理为显示所做的调整和准备工作，无需你进行进一步的交互。

当你的代码需要处理一组源自 `QStandardItem` 的项目时，应使用 `QStandardItemModel`。它是一个相对复杂的类，提供了一组旨在简化列表、表格和树中自定义项目创建的属性。

在处理遗留代码时，你可能会遇到一个名为 `QDirModel` 的遗留类。它与 `QFileSystemModel` 不同，因为它在 GUI 线程上处理文件系统遍历。这可能会对性能产生显著的负面影响

# 使用 Qt 建模数据

学习处理数百个数据项

![](img/c7d3278283754436651c50a2e9c72912_44_0.png)

**上述** 数据展示控件可以分为两组

当需要遍历大量文件和文件夹时，这种影响就会显现出来。

# 模型到模型

大型且复杂的应用程序受益于能够以不同形式显示相同数据集的能力。复制信息会浪费内存，并迫使开发者实现各种同步逻辑。

如果更改仅限于对单个项目的排序和过滤，则可以将代理模型附加到包含实际数据的主模型。它重新排列并过滤元素，以创建对当前信息的独立第二视图。

尽管我们的 `QFileSystemModel` 提供了对结果进行排序和过滤的功能，但我们会为后人和效果添加第二层。

首先，向项目添加一个新类：可以通过文件 > 新建文件或项目调用 Qt Creator 的“添加类”向导。选择 C++ 组以找到 C++ 类模板。示例代码中的新类名为 `ImagineFilterModel` – 如果你愿意，可以随意分配其他名称。头文件看起来像**图 05** 中显示的那样。

`QSortFilterProxyModel` 是一个派生自 QObject 的类。正如你在**图 05** 中所见，Qt 的后端要求此类类的头文件用 Q_OBJECT 宏标记。

`ImagineFilterModel` 的构造函数填充了**图 06** 中的代码片段。

派生自 `QSortFilterProxyModel` 的类需要一个源模型，该模型充当实际数据存储。我们只需分配上述的 `QFileSystemModel` 以准备适配器插入。修改 `mainwindow.cpp` 中表单的构造函数，以便告知其有关 `ImagineFilterModel` 的信息（**图 07**）。

> “ 树视图默认不允许用户对其内容进行排序 ”

```cpp
// Fig 08
class ImagineFilterModel:public QSortFilterProxyModel
{
        Q_OBJECT
public:
        ImagineFilterModel(QObject *parent = 0);
protected:
        bool lessThan(const QModelIndex &left, const QModelIndex &right);
};
```

```cpp
// Fig 09
bool ImagineFilterModel::lessThan(const QModelIndex &left, const QModelIndex &right)
{
        QFileSystemModel* myModel=(QFileSystemModel*)sourceModel();
        QString leftName=myModel->fileName(left);
        QString rightName=myModel->fileName(right);
        if(leftName.compare(rightName)<=0)return true;
        return false;
}
```

```cpp
// Fig 10
MainWindow::MainWindow(QWidget *parent) :
        QMainWindow(parent),
        ui(new Ui::MainWindow)
{
        ui->setupUi(this);
        ImagineFilterModel* myModel=new ImagineFilterModel((QObject*)this);
        ui->treeView->setModel(myModel);
        ui->treeView->setSortingEnabled(true);
}
```

运行当前状态下的程序会生成一个未过滤的树视图，显示你文件系统的内容。让我们继续更改排序顺序，以便文件和文件夹以严格的字母顺序显示（例如，通常给予文件夹对象的优先级除外）。

`QSortFilterProxyModel` 附带排序逻辑。遗憾的是，该类无法控制你希望项目如何排列。这些信息需要通过可以在头文件中重写的一个虚方法传入（**图 08**）。

对于我们的例子，请参见**图 09**，其中找到的比较就足以获得所需的结果。

树视图默认不允许用户对其内容进行排序。可以通过将 `sortingEnabled` 设置为 true 来解决此问题（**图 10**）。

运行当前形式的示例，以查看精心交织的文件和文件夹列表。

# 结论

至此，我们对 Qt 迷人世界的旅程在另一期中结束了。尽管熟悉模型可能需要一点时间，但在这个过程中获得的技能在长期来看会加倍回报，因为结构良好的应用程序更容易调试和维护。最终，它将为节省你的时间和精力。

我们的 Qt 教程的下一部分将把建模再推进一步。我们将学习如何基于应用程序中已存在的数据存储创建自定义模型。随着复杂度的增加，这部分内容将使你能够保持关注点分离。

创建列表和使用树视图从未如此简单 – 我们很快再见！

# 使用 FUZE 学习编写 BASIC 代码

通过 FUZE——由树莓派驱动的编程和电子平台，发现开启这一切的语言

![](img/c7d3278283754436651c50a2e9c72912_45_0.png)

![](img/c7d3278283754436651c50a2e9c72912_45_1.png)

### 顾问

**Rob Zweetsloot** 擅长对复杂系统进行建模，并是一位精通 Python、Django 和 PHP 的 Web 开发者。他喜欢进行计算实验。

### 资源

- FUZE BASIC 套件 [fuze.co.uk](fuze.co.uk)

一代 X 中许多伟大的英国程序员通常被认为得益于 BBC Micro 和 **八十年代的 BBC 计算机通识计划** 而起步。

当时，廉价的硬件学校负担得起，并允许孩子们用“初学者通用符号指令代码”（Beginner’s All-purpose Symbolic Instruction Code）或 BASIC 进行编码。这种简单的语言让学校中所有年龄段的孩子们都能接触编程，并创造了英国的计算热潮。时代略有变化，经过一番挣扎，计算重新回到了英国学校。

虽然他们不再学习 BASIC 了，但该语言仍然存在，并且是教授编程的绝佳方式。FUZE 系列的硬件旨在通过特殊的树莓派驱动机器将其带回来。

你不仅可以编写 BASIC 语言代码，还可以使用连接到 FUZE 设备的优秀自定义 IO 板来创建物理项目。

在本教程中，我们将展示如何使用 BASIC 进行编程以及如何创建交通灯系统。

