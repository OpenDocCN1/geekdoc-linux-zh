

![](img/9bfe0a027fcc8793bb087287001100dd_178_0.png)

**图 5.8** 正在添加项目的字符串列表对话框

```python
def reject(self):
    self.accept()
```

为了测试目的，请在文件末尾添加以下代码：

```python
if __name__ == "__main__":
    fruit = ["Banana", "Apple", "Elderberry", "Clementine", "Fig",
             "Guava", "Mango", "Honeydew Melon", "Date", "Watermelon",
             "Tangerine", "Ugli Fruit", "Juniperberry", "Kiwi",
             "Lemon", "Nectarine", "Plum", "Raspberry", "Strawberry",
             "Orange"]
    app = QApplication(sys.argv)
    form = StringListDlg("Fruit", fruit)
    form.exec_()
    print "\n".join([unicode(x) for x in form.stringlist])
```

这创建了一个 StringListDlg 实例，其中包含一个用于命名列表中事物种类的字符串以及一个字符串列表，然后以模态方式调用它。当用户关闭对话框时，我们在控制台上打印字符串列表，以便查看我们编辑的效果。

你需要阅读 QListWidget 的文档，以及用于获取要添加的字符串和编辑现有字符串的 QInputDialog.getText() 的文档。这个练习大约可以用 120 行代码完成。

参考答案位于文件 chap05/stringlistdlg.py 中。可以通过运行程序来测试它。（在 Windows 上，应从控制台运行；在 Mac OS X 上，应从终端运行。）

- 创建主窗口
- 处理用户操作

# 主窗口

大多数应用程序都是主窗口风格的应用程序，也就是说，它们具有菜单栏、工具栏、状态栏、中心区域以及可能的停靠窗口，旨在为用户提供丰富且易于导航和理解的用户界面。在本章中，我们将学习如何创建一个主窗口风格的应用程序，以展示如何创建和使用所有这些功能。

![](img/9bfe0a027fcc8793bb087287001100dd_179_1.png)

> 图 6.1 图像变更器应用程序

我们将使用图 6.1 中所示的图像变更器应用程序来演示如何创建主窗口风格的应用程序。与大多数此类应用程序一样，它具有菜单、工具栏和状态栏；它还有一个停靠窗口。除了学习如何创建所有这些用户界面元素外，我们还将涵盖如何将用户与这些元素的交互关联到执行相关操作的方法。

本章还解释了如何处理新文件的创建和现有文件的打开，包括使用户界面与应用程序状态保持同步。还涵盖了如何让用户有机会保存未保存的更改，以及如何管理最近使用的文件列表。我们还将展示如何保存和恢复用户偏好设置，包括主窗口以及工具栏和停靠窗口的大小和位置。

大多数应用程序都有一个用于保存数据的数据结构，并通过一个或多个部件让用户查看和编辑数据。图像变更器应用程序在单个 QImage 对象中保存其数据，并使用 QLabel 部件作为其数据查看器。在第 8 章中，我们将看到一个用于呈现和编辑大量数据项的主窗口风格应用程序，在第 9 章中，我们将学习如何创建可以处理多个文档的主窗口应用程序。

在查看如何创建应用程序之前，我们将讨论用户界面必须维护的一些状态。通常，一些菜单选项和工具栏按钮是“可复选”的，也就是说，它们可以处于两种状态之一。例如，在文字处理器中，用于切换斜体文本的工具栏按钮可以是“开”（按下）或“关”。如果还有一个斜体菜单选项，我们必须确保菜单选项和工具栏按钮保持同步。幸运的是，PyQt 使得实现这种同步变得非常容易。

一些选项可能是相互依赖的。例如，文本可以左对齐、居中或右对齐，但在任何时候只能有一个处于“开”状态。因此，如果用户切换了居中对齐，左对齐和右对齐的工具栏按钮和菜单选项必须切换为关。同样，PyQt 使得同步这种相互依赖的选项变得很简单。在本章中，我们将涵盖不可复选的选项，如“打开文件”，以及独立的和相互依赖的可复选选项。

尽管某些菜单和工具栏选项可以立即影响应用程序的数据，但其他选项用于调用对话框，通过它们用户可以精确指定想要执行的操作。由于我们在前 two 章中对对话框进行了大量介绍，因此在这里我们将重点介绍如何使用它们，而不是如何创建它们。在本章中，我们将学习如何调用自定义对话框，以及如何使用 PyQt 的许多内置对话框，包括选择文件名的对话框、打印对话框以及向用户询问数据项（如字符串或数字）的对话框。

# 创建主窗口

对于大多数主窗口风格的应用程序，主窗口的创建遵循相似的模式。我们通过创建和初始化一些数据结构开始，然后创建一个将占据主窗口中心区域的“中心部件”，接着创建并设置任何停靠窗口。接下来，我们创建“动作”并将它们插入到菜单和工具栏中。读取应用程序设置也很常见，对于恢复用户工作区的

![](img/9bfe0a027fcc8793bb087287001100dd_181_0.png)

**图 6.2 图像变更器的模块、类和函数**

应用程序，将加载上次终止时打开的文件。

构成图像变更器应用程序的文件如图 6.2 所示。应用程序的主窗口类位于文件 chap06/imagechanger.pyw 中。初始化器相当长，因此我们将分部分查看它。但首先，让我们查看类定义之前的导入。

```python
import os
import platform
import sys
from PyQt4.QtCore import *
from PyQt4.QtGui import *
import helpform
import newimagedlg
import qrc_resources

_version_ = "1.0.0"
```

在这本书中，惯例是先导入 Python 的标准模块，然后是第三方模块（如 PyQt），最后是我们自己的模块。我们将在代码中使用 os 和 platform 模块中的项时讨论它们。sys 模块通常用于提供 sys.argv。helpform 和 newimagedlg 模块提供 HelpForm 和 NewImageDlg 类。我们将稍后讨论 qrc_resources 模块。

应用程序通常有一个版本字符串，惯例是将其命名为 _version_；我们将在应用程序的关于框中使用它。

现在我们可以查看 MainWindow 类的开头。

```python
class MainWindow(QMainWindow):
    def __init__(self, parent=None):
        super(MainWindow, self).__init__(parent)
```

```python
        self.image = QImage()
        self.dirty = False
        self.filename = None
        self.mirroredVertically = False
        self.mirroredHorizontally = False
```

初始化器以传统的 super() 调用开始。接下来，我们创建一个空的 QImage，我们将用它来保存用户加载或创建的图像。QImage 不是 QObject 的子类，因此不需要父级；相反，我们可以将其删除交给 Python 在应用程序终止时进行正常的垃圾收集。我们还创建了一些实例变量。我们使用 dirty 作为布尔标志来指示图像是否有未保存的更改。filename 最初设置为 None，我们用它来指示要么没有图像，要么有一个从未保存过的新创建图像。

PyQt 提供了各种镜像功能，但对于这个示例应用程序，我们仅限于三种可能性：垂直镜像、水平镜像或不镜像。我们需要跟踪镜像状态，以便保持用户界面同步，当我们讨论镜像操作时将会看到。

```python
        self.imageLabel = QLabel()
        self.imageLabel.setMinimumSize(200, 200)
        self.imageLabel.setAlignment(Qt.AlignCenter)
        self.imageLabel.setContextMenuPolicy(Qt.ActionsContextMenu)
        self.setCentralWidget(self.imageLabel)
```

在某些应用程序中，中心部件是一个复合部件（由其他部件组成的部件，布局方式与对话框中的部件类似）或基于项的部件（如列表或表格），但在这里单个 QLabel 就足够了。QLabel 可以显示纯文本、HTML 或 PyQt 支持的任何图像格式的图像；稍后我们将看到如何发现这些格式，因为它们可能会有所不同。我们设置了最小尺寸，因为最初标签没有内容可显示，因此不会占用空间，这会显得很奇怪。我们选择将图像垂直和水平居中对齐。

PyQt 提供了创建上下文菜单的许多方法，但我们将使用最简单且最常见的方法。首先，我们必须为希望拥有上下文菜单的部件设置上下文菜单策略。然后，我们必须向该部件添加一些动作——这是我们稍后要做的事情。当用户调用上下文菜单时，菜单将弹出，显示已添加的动作。

与使用布局的对话框不同，在主窗口风格的应用程序中，我们永远只有一个中心部件——尽管这个部件可以是复合的，因此实际上没有限制。我们只需要调用 setCentralWidget() 就完成了。该方法既将部件布局在主窗口的中心区域，又将部件重新父化，使主窗口拥有它。

![](img/9bfe0a027fcc8793bb087287001100dd_182_0.png)

