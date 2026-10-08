
## 使用 Qt 处理模型数据

处理十几项数据并不是问题。但如果将数量增加到几百项，问题就可能出现。

![](img/c7d32783754436651c50a2e9c72912_41_0.png)

### 顾问

Tam Hanna 自 Palm IIIc 时代起便涉足 IT 行业。身为记者、导师、演讲者及科学书籍作者，他不仅多次见证了移动市场的各个方面，更对此有着深入的洞察。

虽然没有法律规定禁止你尝试编写此类程序，但你应该意识到，大量令人头疼的问题将会随之而来。首先，请做好准备，接受用户界面极度缓慢且不断刷新的现实，以适应你的用户。

在列表和表格控件的存储中保存大量数据，是招致用户因代码运行缓慢而发怒的必然途径。

如果这还不够让你却步，那么现在你应该知道，在数据管理方面你会遇到各种各样奇怪的问题。对显示记录进行过滤或排序将变成一项真正的艰巨任务。

幸运的是，Qt 提供了一种高效的方式来规避此问题。多年前，一种名为 Smalltalk 的编程语言向世界介绍了模型-视图-控制器（MVC）设计模式的概念。遵循此标准的框架为用户提供专门封装数据存储的类。

显示是通过将它们连接到视图来完成的。你的业务逻辑可以专注于更改屏幕上显示的信息，而无需关心更新控件内部数据存储的繁琐任务。

在 Qt 中，使用模型尤其具有回报。该框架预装了大量可以显示各种有用数据的类。

![](img/c7d32783754436651c50a2e9c72912_41_1.png)

*上图：我们的数据模型为树形视图提供文件系统信息*

让我们从一个创建显示主机计算机文件系统的小型应用程序开始。打开 Qt Creator，并使用“新建项目”向导基于 Qt Widgets 构建一个新项目。双击 `mainwindow.ui`，以便让 Qt Creator 在用户界面设计器中打开该表单。

查看屏幕左侧。你的工具箱应包含两组专门用于显示列表和其他信息的控件：项目视图（item views）和项目小部件（item widgets）。项目小部件为项目提供“嵌入式”存储，而视图必须连接到模型才能正常工作。

### 简化的文件系统

寻求开始使用新编程语言的开发者，最终都会编写一个针对其目标平台文件系统的解析器。这种练习具有极高的教学价值，这也是为什么我们在几期之前带你们完成了这个练习。

引入模型让情况变得容易得多。从工具箱中抓取一个“TreeWidget（树形小部件）”并将其拖到表单的中间。然后，打开 `mainwindow.cpp` 并修改表单的初始化方法，使其看起来像图 01 中的代码。

我们首先调用位于 `ui` 对象中的 `setupUi` 方法。它是由一个名为 `uic`（用户界面编译器）的工具创建的，它充当我们的应用程序与从 UI 文件生成的代码之间的“中介”。

在下一步中，创建了一个 `QFileSystemModel` 的新实例。通过将其设为表单的子对象，我们确保父子系统会在用户决定关闭相应窗口时移除该实例。调用 `setRootPath` 通知模型需要处理特定的路径。

## 使用 Qt 处理模型数据

学习处理数百个数据项

![](img/c7d32783754436651c50a2e9c72912_42_0.png)

### 模型-视图-控制器

### 拆解大型系统

按照预定义的步骤整理系统有助于新开发者更快上手。这是通过一组如今被称为设计模式的架构来实现的。模型-视图-控制器（MVC）模式是最古老的之一——它诞生时“设计模式”这个术语尚未形成。

基于 MVC 的应用程序由三个部分组成。模型包含需要被使用和管理实际数据。大多数实现还将业务逻辑也放置在其中。模型中发生的更改可以推送到“感兴趣的观察者”。

模型数据在视图中渲染和显示。视图知道提供信息的控制器和模型，但通常不包含处理用户输入的任何逻辑。尽管视图通常负责实际的渲染，但它们通常不直接操作数据（用于过滤等）。

控制器充当上述两个对象之间的“胶水”。它们通常负责过滤和排序，此外还处理用户输入。一些实现在控制器和模型之间分担输入处理的负担：如果后者包含业务逻辑，那么如果必须在控制器中处理所有输入，就会发生重复。

```cpp
#include <QFileSystemModel>

MainWindow::MainWindow(QWidget *parent) :
	QMainWindow(parent),
	ui(new Ui::MainWindow)
{
	ui->setupUi(this);

	QFileSystemModel *myModel = new QFileSystemModel(this);
	myModel->setRootPath("/");
	ui->treeView->setModel(myModel);
}
```

至此，模型已准备好分配给视图。这是通过调用 `treeView` 的 `setModel` 方法来实现的。你可以自由地在当前状态下运行该应用——在 Unix 操作系统上运行时，树将显示机器上找到的文件和文件夹的可展开列表。

事实上，`QFileSystemModel` 甚至为你处理了多线程。文件系统遍历由后台线程处理，并将结果推送到 GUI。遗憾的是，这意味着代码背后的存储数据无法立即访问——你应该等待直到 `rowCount()` 属性停止返回零。

### 让模型发挥作用

尽管显示文件系统的内容绝非易事，但我们的 `QFileSystemModel` 能够完成更多任务。例如，让我们添加一个名称过滤器，以确保树只包含 JPG 文件。

```cpp
MainWindow::MainWindow(QWidget *parent) :
	QMainWindow(parent),
	ui(new Ui::MainWindow)
{
	ui->setupUi(this);

	QFileSystemModel* myModel = new QFileSystemModel(this);
	myModel->setRootPath("/");
	QStringList *myStringList = new QStringList();
	myStringList->append("*.jpg");
	myStringList->append("*.jpeg");
	myModel->setNameFilters(*myStringList);
	myModel->setNameFilterDisables(false);
	ui->treeView->setModel(myModel);
}
```

```cpp
#include <QModelIndex>

class MainWindow : public QMainWindow
{
	Q_OBJECT
public slots:
	void itemDoubleClicked(QModelIndex _anIndex);
	.
.
.
```

这可以通过再次修改主表单的构造函数来实现。该方法的新版本看起来像图 02 中的示例。

`QStringList` 是框架提供的辅助类，专门用于管理一组字符串。我们的示例代码创建一个空实例，并继续向其中添加两个包含正则表达式的字符串。生成的复杂对象随后被传递到 `setNameFilters`，在那里它被用于参数化遍历函数。将 `nameFilterDisables` 设置为 `false` 确保不匹配模式的结果不被显示——传递 `true` 会使它们以灰色显示。

至此，我们的文件树现在仅限于显示伪装成图片的文件。再次运行应用程序，以确认非图像文件不再在树形视图中显示。

### 访问模型数据

基于模型-视图-控制器模式的应用程序并不限于显示模型中找到的数据。实现良好的模型类提供了多种方式，允许用户与存储在内的数据进行交互——我们的 `QFileSystemModel` 也不例外。

让我们通过添加一个功能来扩展我们的文件查看器，该功能提供有关双击项目的更多信息。这需要我们将树形视图的 `doubleClicked` 信号与主表单中新创建的槽连接起来。

点击工具栏中的信号/槽编辑器，以告知 Qt Creator 你打算创建信号和槽之间的连接。从树形视图拖出一条线并将其放到表单上。Qt Creator 会响应并打开

