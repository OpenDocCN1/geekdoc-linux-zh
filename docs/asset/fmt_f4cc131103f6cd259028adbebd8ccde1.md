
任何使用 `Boost.Build` 构建的应用程序都需要两个文件：`boost-build.jam` 和 `Jamroot`。实际上，任意数量的应用只需要一份 `boost-build.jam` 拷贝，只要它位于所有应用程序目录（无论嵌套多深）所在的目录下。`boost-build.jam` 文件只需要包含一行，用于指定构建系统安装目录的路径。例如：

```
boost-build /home/kathy/opt/boost-build ;
```

构建 `Spreadsheet` 应用所需的 `Jamroot` 文件如下：

```
using qt :/home/kathy/opt/qt432 ;

exe spreadsheet:
cell.cpp
finddialog.cpp
finddialog.h
gotocelldialog.cpp
gotocelldialog.h
gotocelldialog.ui
main.cpp
mainwindow.cpp
mainwindow.h
sortdialog.cpp
sortdialog.h
sortdialog.ui
spreadsheet.cpp
spreadsheet.h
spreadsheet.qrcode
/qt/Qt
/qt/QtCore ;
```

第一行引入了 `Qt 4` 支持，我们必须提供 `Qt 4` 的安装路径。接下来，我们指定要构建一个名为 `spreadsheet` 的可执行文件，并且它依赖于列出的文件。对于头文件，`Boost.Build` 足够智能可以识别其依赖关系，通常不需要列出它们。然而，定义 `Q OBJECT` 类的 h 文件必须由 `moc` 处理，因此我们必须将它们包含在列表中。最后两行指定了我们要使用的 `Qt` 库。

假设 `bjam` 可执行文件在路径中，我们可以使用以下命令构建应用程序：

```
bjam release
```

## 602

### B. 构建 Qt

这告诉 `Boost.Build` 使用 `release`（发布）模式构建当前目录下 `Jamroot` 文件中指定的应用程序。（如果你只安装了 `Qt` 的调试库，这将产生错误；在这种情况下请运行 `bjam debug`。）`moc`、`uic` 和 `rcc` 工具将根据需要运行。清理时，请运行 `bjam clean`。

## SCons: 软件构建工具

`SCons` 工具可在 `http://www.scons.org/` 获取，是一个基于 `Python` 的开源工具，旨在取代 `make`。它对 `Qt 3` 有内置支持，并且可以从 David García García 在 `http://www.uia.upf/~dgarcia/Codders/sools.html` 处获取支持 `Qt 4` 的插件。需要从该网站下载一个文件 `qt4.py`，它应该与应用程序存放在相同的目录下。该扩展预计在不久后会被包含在 `SCons` 的官方发布中。

一旦 `qt4.py` 准备就绪，我们可以创建一个 `SConstruct` 文件来指定我们的构建配置：

```
#!usr/bin/env python

import os

QT4_PATH = ""
QTDIR = "/home/kathy/opt/qt432"

pkgpath = os.environ.get("PKG CONFIG PATH", "")
pkgpath += " :%s/lib/pkgconfig" % QTDIR
s.environ["PKG CONFIG_PATH"] = pkgpath
os.environ["QTDIR"] = QTDIR
```

```
env = Environment(tools="default", toolpath=[QT4_PY_PATH])
env["CXXFILESUFFIX"] = ".cpp"

env.EnableQtModules("QtGui", "QtCore")
rcs = [env.Qrc("spreadsheet.qrc", Qt4FLAGS=-name spreadsheet)]
uis = [env.Ui for ui in ["gotocellialog.ui", "sortdialog.ui"]]
sources = [
"cell.cpp",
"finddialog.cpp",
"gotocellialog.cpp",
"main.cpp",
"mainwindow.cpp",
"sortdialog.cpp",
"spreadsheet.cpp"
]
env.Program(target="spreadsheet", source=[rccs, sources])
```

该文件是用 `Python` 编写的，因此我们可以使用 `Python` 语言提供的特性和库。

文件的大部分是模板代码，只需要几个特定的应用程序项。通过设置 `qt4.py` 和 `Qt 4` 安装目录的路径，我们通过将 `qt4.py` 放在标准位置并相应设置路径，避免了将其拷贝到每个应用程序目录中。我们必须显式启用正在使用的 `Qt` 模块（在本例中 `QtCore` 和 `QtGui`），并且指定需要由 `rcc` 或 `uic` 处理的文件。最后，我们列出源文件，并设置程序名称以及它依赖的源和资源文件。我们不需要指定 `.h` 文件；`Qt 4` 支持足够智能，可以通过检查 `.cpp` 文件在需要时正确运行 `moc`。

现在我们可以使用 `scons` 命令构建应用程序了：

```
scons
```

这将构建当前目录下 `SConstruct` 文件中指定的应用程序。我们可以使用 `scons -c` 进行清理。

- `Qt Jambi` 入门
- 在 `Eclipse IDE` 中使用 `Qt Jambi`
- 使用 `Qt Jambi` 集成 C++ 组件

## Qt Jambi 简介

`Qt Jambi` 是 `Qt` 应用程序开发框架的 `Java` 版本。`Qt Jambi` 的核心是构成 `Qt` 的 C++ 库，这些库通过 `Java Native Interface (JNI)` 为 `Java` 程序员提供。尽管付出了大量努力让 `Jambi` 与 `Java` 无缝集成，并使其 `API` 对 `Java` 程序员来说自然易用，但 C++ 程序员仍然会觉得该 `API` 熟悉且可预测。所有类都使用 `http://doc.tolltech.com/qtambiget` `Javadoc` 文档。

到目前为止，`Qt GUI` 程序员一直不得不处理 `AWT`、`Swing` 和类似的 `GUI` 类库，其中没有任何一个像 `Qt` 那样易于使用或功能强大。在传统的 `GUI` 库中，用户操作（如点击按钮）对应的方法涉及编写事件监听器；在 `Qt Jambi` 中，只需一行代码即可实现相同的功能。而且 `Qt` 的布局管理器比 `Swing` 的 `BoxLayout` 和 `GridBagLayout` 容易使用得多，并且产生的视觉效果更好。

## Qt Jambi 入门

在本节中，我们将开发一个小型 `Java` 应用程序，该程序将在 C.1 节中展示的窗口。除了窗口标题外，`Jambi` 查找对话框（Find dialog）的外观和行为与我们在第 2 章中创建的查找对话框相同。通过重用同一个示例，我们可以更容易看到 C++/`Qt` 与 `Qt Jambi` 之间的差异和相似之处。在查看代码时，我们将讨论 C++ 和 `Java` 之间的概念差异。

`Jambi` 查找应用的实现在名为 `FindDialog.java` 的单个文件中。我们将从导入语句开始逐部分查看该文件的内容。

```
import com.trolltech.qt.core.*;
import com.trolltech.qt.gui.*;
```

它们之间的两个导入语句使得 `Qt` 的核心和 `GUI` 接口对 `Java` 可用。其他的类可以通过类似的导入语句可用（例如 `import com.trolltech.qt.opengl()`）。

```
public class FindDialog extends QDialog {
```

`FindDialog` 类是 `QDialog` 的子类，类似于 C++ 版本的示例。我们在头文件中声明信号，依靠 `moc` 工具生成支持代码。在 `Jambi` 中，使用 `Java` 的反射机制来实现信号槽机制。但我们仍然需要声明信号，这是通过 `SignalW` 类完成的：

```
public Signal2<String, Qt.CaseSensitivity> findNext =
    newSignal2<String, Qt.CaseSensitivity>();

public Signal2<String, Qt.CaseSensitivity> findPrevious =
    newSignal2<String, Qt.CaseSensitivity>(),
```

共有十个 `SignalW` 类——`Signal0`、`Signal1T1` 直到 `Signal9T1,...,T9`。它们的数字表示它们的参数的数量以及参数的类型。在这里，我们声明了两个信号，

## 开始使用 Qt Jambi

每个都接收两个参数。在这两种情况下，第一个参数都是一个 `Java` `String`，第二个参数的类型为 `Qt.CaseSensitivity`，这是一个 `Java` 枚举。在 `Qt API` 中需要 `QString` 的地方，在 `Qt Jambi` 中我们使用 `String` 代替。

与其他的信号/槽类不同，`Signal0` 不是一个泛型类。要创建一个没有参数的信号，我们如下所示使用 `Signal0`：

```java
public Signal0 somethingHappened = new Signal0();
```

在创建了需要的信号后，我们现在准备好查看构造函数的实现。该方法相当长，因此我们将分三部分来看。

```java
public FindDialog(QWidget parent) {
    super(parent);
    label = new QLabel(tr("Find &what:"));
    lineEdit = new QLineEdit();
    label.setBuddy(lineEdit);

    caseCheckBox = new QCheckBox(tr("Match &case"));
    backwardCheckBox = new QCheckBox(tr("Search &backward"));

    findButton = new QPushButton(tr("Find &next"));
    findButton.setEnabled(false);

    closeButton = new QPushButton(tr("Close"));
}
```

在 `Java` 中创建小组件与 C++ 相比唯一的区别在于语法上的细微差别。注意 `tr()` 返回的是一个 `String`，而不是 `QString`。

```java
lineEdit.textChanged.connect(this, "enableButton(String)");
findButton.clicked.connect(this, "clicked()");
closeButton.clicked.connect(this, "reject()");
```

`Qt Jambi` 中信号-槽连接的语法与 C++/`Qt` 有些不同，但它短小且简单。通常，语法为：

```java
sender.signalName.connect(receiver, "slotName(T1, ..., TN)");
```

与 C++ 不同，我们不需要为信号指定签名。如果信号的参数比它所连接的槽多，则额外的参数将被忽略。此外，在 `Qt Jambi` 中，信号-槽机制不仅限于 `QObject` 的子类；任何继承 `EventEmitter` 的类都可以发射信号，任何类的任何方法都可以作为槽。

```java
QHBoxLayout layoutToLeftLayout = new QHBoxLayout();
topLayout.addWidget(label);
topLayout.addWidget(lineEdit);

QVBoxLayout leftLayout = new QVBoxLayout();
leftLayout.addLayout(topLayout);
leftLayout.addWidget(caseCheckBox);
leftLayout.addWidget(backwardCheckBox);
```

## 608

## C. Qt Jambi 简介

```java
QVBoxLayout rightLayout = new QVBoxLayout();
rightLayout.addWidget(findButton);
rightLayout.addWidget(closeButton);
rightLayout.addStretch();

QHBoxLayout mainLayout = new QHBoxLayout();
mainLayout.addLayout(leftLayout);
mainLayout.addLayout(rightLayout);
setLayout(mainLayout);
setWindowTitle(tr("Jambi Find"));
setFixedHeight(sizeHint().height());
```

布局代码与 C++ 原版完全相同，相同的布局类以完全相同的方式工作。`Qt Jambi` 还可以使用 `Qt Designer` 使用表单，配合 `juic`（`Java` 接口编译器），我们将在下一节中看到。

```java
private void findClicked() {
  String text = edit.text();
  CaseSensitivity cs = checkBox.isChecked() ? Case.CaseSensitive : Case.CaseInsensitive;
  if (backwardCheckbox.isChecked()) {
    findPrevious.emit(text, cs);
  } else {
    findNext.emit(text, cs);
  }
}
```

`Java` 引用枚举值的语法比 C++ 稍微冗长一点，但很容易理解。要发射信号，我们调用 `Signal` 对象的 `emit()` 方法并传递正确类型的参数。类型检查在程序编译时完成。

```java
private void enableFindButton(String text) {
  findButton.setEnabled(text.length() == 0);
}
```

`enableFindButton()` 方法基本上与 C++ 原版相同。

```java
private QLabel label;
private QLineEdit editEdit;
private QCheckBox checkBox;
private QCheckBox backwardCheckbox;
private QPushButton findButton;
private QPushButton closeButton;
```

为了保持书中其余部分的代码风格，我们将所有小组件都声明为类的私有字段。这纯粹是一个风格问题；并没有阻止我们在构造函数中声明那些仅在构造函数中引用的组件。例如，我们可以在构造函数中声明 `label` 和 `closeButton`，因为它们在其他地方没有被引用，并且在构造函数结束时不会被垃圾回收。`Qt Jambi` 使用与 C++/`Qt` 相同的父子所有权机制，因此一旦 `label` 和控件布局，`FindDialog` 就会获得它们的所有权，并在后台保留它们的引用以保持存活。如果删除了一个顶级窗口，`Qt Jambi` 会递归地删除子组件，窗口反过来删除其所有子组件和布局，布局再删除它们，以此类推，直到清理完成。

`Qt Jambi` 充分利用了 `Java` 的垃圾回收功能，与 `AWT`、`Swing` 和 `SWT` 不同，如果顶级窗口的最后一个引用被删除，该窗口将被安排垃圾回收，而不需要显式调用 `dispose()`。这种方法非常方便，且工作方式与 C++/`Qt` 相同。主要的注意事项对于 SDI（单文档界面）应用程序，我们必须保留每个创建的顶级窗口的引用，以防止它们被垃圾回收。（在 C++ 中，SDI 通常使用 `Qt::WA DeleteClose` 属性来防止内存泄漏。）

```java
public static void main(String[] args) {
    QApplication.initialize(args);
    FindDialog dialog = new FindDialog(null);
    dialog.show();
    QApplication.exec();
}
```

## 开始使用 Qt Jambi

## 使用 Java 资源系统

与许多 `Java` 标准类不同，`Qt Jambi` 完全感知 `Java` 的资源系统。`Java` 资源通过 `classpath:` 前缀进行标识。在 `Qt Jambi API` 中任何可以使用文件名的地方，都可以指定 `Java` 资源。例如：

```java
QIcon icon = new QIcon("classpath:/images/icon.png");
if (!icon.isNull()) {
}
```

为了找到图标，`Qt Jambi` 将查找 `CLSPATH` 环境变量指定的目录或 `.jar` 文件中的 `images` 目录。一旦找到了图像文件 `icon.png`，搜索就会停止并使用该文件。如果没有找到文件，不会抛出异常。在上面的示例中，如果找不到图标，`icon.isNull()` 将返回 `true`。像 `Qimage` 和 `QPixmap` 这样具有带有文件名参数构造函数的类有一个 `isNull()` 方法，可以通过测试它来检查文件是否成功读取。在 `QFile` 的情况下，我们可以检查 `QFile.error()` 来查看文件是否已读取。

# 开始使用 Qt Jambi

`Java`应用程序，不同之处是 `CLASSPATH` 环境变量必须指定 `Qt Jambi` 安装的目录。我们必须使用 `Java` 编译器编译该类，然后就可以使用 `Java` 解释器执行该类。例如：
