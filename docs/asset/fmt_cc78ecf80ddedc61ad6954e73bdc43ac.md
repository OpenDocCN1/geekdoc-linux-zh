
虽然编写信号槽函数以及建立连接对程序员来说可能看起来很简单，但实际上需要更复杂的 `C++` 代码。信号槽函数需要经过元对象编译器（`MOC`）预处理，以生成实现信号槽消息连接过程的 `C++` 代码。你随后将 `MOC` 的输出包含在源文件中。这意味着你应该将具有信号和槽的类声明放在单独的头文件中。

你不能将成员函数定义与类声明合并。为了编译，类声明必须先经过 `MOC` 的预处理，然后正确地与成员函数定义结合。这要求将类声明放在与函数独立的文件中，以便对类声明进行单独 `MOC` 预处理。

# 358 Linux 编程：入门指南

| 选项 | 描述 |
| :--- | :--- |
| `-o file` | 将输出写入文件而非 `STDOUT`。强制在输出中生成一个 `#include` 语句。只有当您的头文件不符合标准命名规范时，此选项才有用处。 |
| `-l` | 不在输出中生成 `#include` 语句。此时您应该在 `.cpp` 文件中 `#include` 该元对象代码。 |
| `-nw` | 不生成任何警告。 |
| `-ldbg` | 在 `STDOUT` 上写入词法调试信息。为了内部调试，将所有缺失的成员视为槽（slots）。 |
| `-p path` | 使 `MOC` 在生成的 `#include` 语句中在文件名前加上 `path/`。 |
| `-q path` | 使 `MOC` 在生成的代码中在 `Qt` `#include` 文件名前加上 `path/`。 |

表 10-2 `MOC` 选项

要声明一个包含信号或槽的类，您首先需要在头文件 `myobj.h` 中声明该类。您不需要在头文件中放置任何成员函数的定义，只保留类声明。请注意，类声明将包含成员函数、结构体变量的声明。在另一个源文件中，您将放置成员函数的定义，例如 `myobj.cpp`。成员函数的定义是该函数的实际代码。

为了让这些定义被正确编译，您必须包含其对象声明的 `MOC` 预处理版本，而不是本身。要生成预处理后的 `MOC` 版本，您可以使用类声明头文件和 `moc` 命令，如下所示：

```
moc myobj.h -o myobj.moc
```

在为该对象定义成员函数的特定源文件中，您应该包含包含对象声明的头文件的 `MOC` 版本，而不是头文件本身。您应该在 `myobj.cpp` 源文件中包含 `myobj.moc`，而不是 `myobj.h`。

然而，对于任何其他生成该类实例的源文件（例如通过新操作生成），您只需要包含头文件，而不需要包含 `MOC` 文件：因此，对于任何只需要类声明的源文件 `m`，您都包含头文件，例如 `myobj.h`。

例如，假设在 `main.cpp` 文件中生成了一个 `myobj` 对象作为变量，而在 `myobj.cpp` 文件中有 `myobj` 类的成员函数定义。此外，假设 `myobj` 的类定义在 `myobj.h` 头文件中，而 `myobj.h` 的 `MOC` 版本在 `myobj.moc` 文件中。在 `main.cpp` 文件中，您将包含 `myobj.h` 文件（而不是 `myobj.moc`），但在 `myobj.cpp` 文件中，您将包含 `myobj.moc` 文件（而不是 `myobj.h`）。

# 项目 10-1：一个 KDE 窗口

`hellowin.cpp` 是一个简单的程序，它在主窗口中显示一个按钮，点击时显示“Hello World”消息。`Hellowin` 声明了两个槽：`myhello`（显示消息）和 `myexit`（退出程序）。声明还应包含 `Q_OBJECT`，`Q_OBJECT` 是 `KDE` 用于连接到 `Qt` 工具包的特殊对象。`Hellowin` 的声明将放在 `hellowin.h` 头文件中，所有的成员函数定义将放在 `hellowin.cpp` 文件中。

要编译此程序，您首先需要用 `MOC` 预处理 `hellowin.h` 头文件。然后，您可以编译 `hellowin.cpp` 文件。注意，此文件应该包含 `hellowin.moc` 文件，而不是 `hellowin.h` 文件。编译操作如下：

```
先用 moc 处理头文件再用 C++ 编译器 g++ 
```

```
moc -o hellowin.moc hellowin.h
g++ -lkdecore -lkdeui -lqt -o hellowin hellowin.cpp
```

根据您的系统，您可能还需要指定 `KDE` 库和头文件的位置。这些通常存储在 `KEDIR` 变量指定的 `KDE` 目录。使用 `-L` 选项配合 `/lib` 目录指定库，使用 `-I` 选项配合 `/include` 目录指定头文件，例如 `-LKEDIR/lib` 和 `-IKEDIR/include`。如果未设置 `KEDIR`，请咨询系统管理员或查看 `Linux` 发行版手册获取 `KDE` 库和头文件的位置。这里显示了一个指定 `KDE` include 和 lib 目录位置的编译示例：

```
g++ -LKEDIR/lib -IKEDIR/include -lkdeui -lqt -o hellowin hellowin.cpp
```

## 注意

一种更好的组织方式是将成员函数定义放在单独的源文件中，将主函数留在它自己的源文件中。在这种情况下，您在包含主函数的地方包含 `hellowin.h`，在包含成员函数定义的地方包含 `hellowin.moc`。“Hello World”消息将由 `QMessageBox` 对象处理。该类实现了一个带有消息和若干按钮（如果需要的话）的简单对话框。除了简单的对话框外，`QMessageBox` 还支持带有是、否和取消按钮的对话框。务必包含 `msgbox.h`。对于关于（About）框，您可以使用 `KAboutDialog`。

# 步骤说明

1. 创建 `hellowin.h` 头文件，用于存放 `Hellowin` 类的定义。

2. 包含包含窗口、按钮和消息框等对象类定义的头文件。在这种情况下，包含主窗口的头文件 `kmainwindow.h`；按钮的 `pushbutton.h`；以及消息框的 `msgbox.h`。

3. 定义派自 `KMainWindow` 的 `Hellowin` 类。给 `Hellowin` 类定义两个槽（函数）：`myhello` 和 `myexit`。定义两个指向按钮的指针：`buttonhi` 和 `buttonExit`。

4. `hellowin.cpp` 文件将存放主程序。首先包含头文件和 `hellowin.moc` 文件，这些需要由 `MOC` 预处理器单独生成。

5. 为 `Hellowin` 定义一个构造函数。当定义该类的对象时，该函数会自动执行。

6. 使用 `QPushButton` 创建一个按钮指针，并将其分配给 `buttonhi` 指针。设置其大小并显示它。它连接到 `myhello`，因此点击它时会执行 `myhello` 函数。

7. 使用 `QPushButton` 创建另一个按钮对象，并将其分配给 `buttonExit` 指针。设置其大小并显示它。连接到 `myexit`，因此点击它时将执行 `myexit` 函数。

8. 为 `Hellowin` 类定义一个 `closeEvent` 函数。该函数应通过调用 `kapp->quit` 简单结束程序。

（此处原文已中断）

```cpp
void Hellowin::myhello()
{
    KMsgBox::message(0,"Important","Hello World!");
}

void Hellowin::myexit()
{
    close();
}

int main(int argc, char **argv)
{
    KApplication myapp (argc, argv, "Hello World!");
    Hellowin mywin;
    mywin.setGeometry(100,100,200,100);

    myapp.setMainWindow(&mywin);
    mywin.show();
    return myapp.exec();
}
```

# 菜单

要创建菜单，你需要创建一个 `KDE` 菜单栏，并将带有菜单项的 `Qt` 菜单添加到其中。你需要为菜单包含 `qpopupmenu.h` 头文件，并为菜单栏包含 `kmenu.h` 头文件，如下所示：

```cpp
#include <qpopupmenu.h>
#include <kmenu.h>
```

然后你定义一个菜单栏或指向菜单栏的指针，并对菜单执行相同的操作。菜单栏的类是 `KMenuBar`，菜单的类是 `QPopupMenu`。以下示例定义了菜单栏和一个菜单的指针：

| 定义一个指向的指针 | |
| --- | --- |
| `KMenuBar *menubar;` | `KMenuBar` 类型的对象 |
| `QPopupMenu *myfile;` | |

如果你定义了指针，可以使用 `new` 操作创建菜单和菜单栏对象，如下所示。`KMenuBar` 接受父对象作为参数。在像窗口这样的类中定义时，如果你希望该类本身成为父对象，则使用此指针。

```cpp
mymenubar = new KMenuBar(this);
myfilemenu = new QPopupMenu;
```

然后，你可以通过菜单栏的 `insertItem` 成员函数将菜单添加到菜单栏中。第一个参数是你想在菜单栏上显示的菜单标签，第二个参数是菜单对象的地址。以下示例将 `myfilemenu` 添加到 `mymenubar`：
