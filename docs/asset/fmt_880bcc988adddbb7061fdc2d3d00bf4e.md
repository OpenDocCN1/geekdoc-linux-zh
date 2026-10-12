
表 10-1 常见的 KDE 2.0 `kdeui`（用户界面）续

## KDE 应用程序和小部件

要创建一个 KDE 应用程序，你只需要在定义其他对象之前创建一个 `KApplication` 对象。`KApplication` 的类声明包含在 `kapp.h` 文件中。`K` 对象的定义接收 `argc` 和 `argv` 作为参数。这些参数的操作与 C 程序相同，引用用户输入的任何命令行参数。以下示例定义了一个名为 `myapp` 的对象：

```cpp
KApplication myapp(argc, argv);
```

不同类型的 KDE 和 Qt 对象声明位于不同的头文件中。每当你定义特定类型的对象时，务必包含其类声明所在的头文件。例如，为了创建一个主窗口，你使用 `KMainWindow` 类，并且需要包含 `kmainwindow.h` 头文件。

```cpp
#include <kmainwindow.h>
```

头文件作为参考源也非常有用。它们列出了特定类的所有成员函数，并包含了描述每个函数及其用途的详细注释。头文件位于 KDE 目录 `/usr/include`。目前对于 Red Hat，这是标准包含目录，而在 Linux 和其他发行版中，它可能是特殊的 KDE 目录，例如 `/opt/kde/include`。

为你的应用程序定义主窗口，使用 `KMainWindow` 类。以下示例定义了一个名为 `mywin` 的主窗口对象：

```cpp
KMainWindow mywin;
```

如果你创建一个以主窗口作为主要界面的应用程序，并且希望在窗口关闭时关闭应用程序，你需要为应用程序设置主部件。要实现这一点，请使用应用程序对象的 `setMainWidget` 函数。主部件可以是你想要的任何小部件。务必传递该部件的地址。你通过在它前面加上地址操作符 `&` 来实现。

## 352 Linux 编程：初学者指南

以下示例将主部件设置为 `mywin` 窗口。

传递了 `mywin` 部件的地址：`&mywin`。

```cpp
app.setMainWidget(&mywin);
```

> **提示**
>
> 如果你对部件使用指针（如在本模块的稍后的程序示例中所示），你只需要传递指针，而无需使用地址操作符。指针已经持有了地址。

当你定义一个部件时，你也会定义包含在它的类声明中的任何成员函数。请参阅 `developer.kde.org` 文档以获取关于所有 KDE 类声明的完整描述，包括它们的成员函数。这些成员函数中许多旨在更改部件的显示特征，例如其颜色或初始大小。要控制 `KMainWindow` 部件的显示大小，你使用它的 `setGeometry` 函数，如下所示：

```cpp
mywin.setGeometry(100, 100, 200, 100);
```

你必须显式指示 KDE 显示任何想要显示的部件。要做到这一点，你使用部件的 `show` 成员函数。例如，为了让 `mywin` 窗口显示，你执行它的 `show` 函数，如下所示：

```cpp
mywin.show();
```

一旦你定义了所有的部件并进行了任何修改，你就可以运行应用程序。你通过 `QApplication` 对象的 `exec` 成员函数来实现。

```cpp
app.exec();
```

当用户关闭应用程序时，控制权返回到主函数，主函数可以终止程序。通常 `exec` 函数的返回语句将返回 `exec` 可能产生的任何错误。

```cpp
return app.exec();
```

以下程序创建一个显示窗口的简单 KDE 。图 10-1 显示了该程序显示的窗口。

```cpp
#include <kapp.h>
#include <ktmainwindow.h>

int main(int argc, char **argv) {
    KApplication myapp(argc, argv); // 定义 myapp 
    KTMainWindow mywin;
    mywin.setGeometry(100, 100, 200, 100);

    myapp.setMainWidget(&mywin); // 定义 mywin 窗口
    mywin.show();
    return myapp.exec();
}
```

## 1分钟快速练

- KDE 程序是用 C++ 编写的吗？
- 你使用哪个类来定义应用程序的主窗口？

![](img/3cfc28f62e3fe98d5a49b453e25d689c_376_0.png)

- 是
- `KDMainWindow`

## 专家问答

**问题：** 我如何编译 KDE 程序？

**回答：** 你就像编译任何 C++ 程序一样编译 KDE 程序。使用 `g++` 命令并指定要使用的 KDE 和 Qt 库。

**问题：** 如果我收到编译器找不到头文件 (.h) 的错误怎么办？

**回答：** 这通常意味着编译器不知道 KDE 或 Qt 库在系统上的位置。你可以使用 `-I` 选项指定头文件目录，并使用 `-L` 选项指定包含库的目录。例如，如果你的 KDE 头文件位于 `/opt/kde/include` 目录，你将使用：

```bash
-I/opt/kde/include
```

**问题：** 是否有更简单的方法指定 `KEDIR` 以及头文件和库的位置？

**回答：** 是的，许多系统已经设置了 `KEDIR` 和 `QTDIR` 环境变量。`KEDIR` 包含 KDE 命令、头文件和库的路径名称，`QTDIR` 包含 Qt 的路径名称。要指定 KDE 的头文件，你将使用：

```bash
-I$KEDIR/include
```

务必在 `KEDIR` 之前包含 `$`。如果 `KEDIR` 尚未定义，你可以自己定义它，分配 KDE 组件的位置（如果你知道的话）：

```bash
KEDIR = /opt/kde
```

在 Red Hat Linux 中，6.0 版本的 Qt 库被放置在 `/usr/lib/qt` 目录，而 KDE 库与 `/usr/lib` 目录中的其他库混合在一起。你不需要指定 KDE 库；对于 Qt，你指定 `/usr/lib/qt` 目录。Caldera OpenLinux 以及其他发行版目前定义 KDE 库位于 `/opt/kde` 目录。

在以下示例中，为 `myapp.cpp` KDE 程序同时指定了 KDE 和 Qt 库。

```bash
g++ -I$KEDIR/include -L$KEDIR/lib -I$QTDIR/include -L$QTDIR/libs -lkcore -lkdeui -lqt myapp.cpp
```

**问题：** 我如何在 `myfile` 中设置这些库和目录规范？

**回答：** 记住，`myfile` 是为了编译由多个不同源文件组成的程序设计的。每个文件都被单独编译，然后由链接器（Linker）将编译后的版本组合成可执行的应用程序文件。要编译源文件，你需要指定头文件，如下所示。

```bash
g++ -c -I$KEDIR/include -I$QTDIR main.cpp
```

要使用链接器创建应用程序，你需要指定 KDE 库的目录、你想使用的特定 KDE 库以及 Qt 库。在这个示例中，使用了 `kdecore` 和 `kdeui` 库。这些是 KDE 核心库和 KDE 用户界面库。Qt 是 Qt 库。

```bash
g++ -L$KEDIR/lib -I$QTDIR/include -lkcore -lkdeui -lqt myapp main.o
```

## 信号与槽

KDE 和 Qt 使用信号和槽允许部件与另一个部件进行通信。信号和槽是类中定义的具有特殊能力的成员函数。当事件发生时，对象发射信号。

槽是响应信号的成员函数。要将信号连接到槽，你使用 `connect` 函数。第一个参数是对象，第二个是信号，第三个是槽。要指定信号，使用 `SIGNAL` 宏。对于回调函数，使用 `SLOT` 宏。通过 `connect` 操作，你可以将一个信号连接到多个槽。

| 信号发生的对象 | 部件上的信号 | 对象中的函数 |
| :--- | :--- | :--- |
| `buttonhi` | `clicked()` | `myhello()` |

```cpp
connect(buttonhi, SIGNAL(clicked()), mywin, SLOT(myhello()));
```

由多个部件组成的类（例如应用程序窗口）通常会有不同部件到主部件的连接。连接操作通常位于主部件类的声明中。在这种情况下，主部件（对象）可以使用 C++ 指针引用，它始终引用定义的类，如下所示：

```cpp
connect(buttonhi, SIGNAL(clicked()), this, SLOT(myhello()));
```

## 提示

任何包含槽或信号的类都必须包含一个名为 `Q_OBJECT` 的特殊引用。这使得元对象编译器预处理器（下文描述）能够设置类中声明的任何信号和槽。

## 元对象编译器：MOC
