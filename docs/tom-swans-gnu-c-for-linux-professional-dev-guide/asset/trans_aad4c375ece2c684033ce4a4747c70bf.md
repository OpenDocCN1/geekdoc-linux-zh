

## 第30章 使用 V 开发 X 软件

along with many of those described in this chapter. 要使用一个类，将其头文件包含到你的程序模块中。有关这些及其他 V 类的更多信息，请使用你的 Web 浏览器打开 V 的在线文档，从文件 `v/vrefman/index.html` 开始。

**表 30.1：V 的主要类**

| Class | Header File | Creates |
| --- | --- | --- |
| `vApp` | `vapp.h` | Main application |
| `vBrush` | `vbrush.h` | Painting (fill) brush |
| `vCanvasPane` | `vcanvas.h` | Window drawing canvas |
| `vCmd` | `vcmd.h` | Dialog and toolbar object |
| `vCmdWindow` | `vcmdwin.h` | Command (main or child) window |
| `vColor` | `vcolor.h` | Standard color object |
| `vCommandPane` | `vcmdpane.h` | Toolbar (pane) |
| `vDC` | `vdc.h` | Device (graphics) context |
| `vDialog` | `vdialog.h` | Modeless dialog box |
| `vFont` | `vfont.h` | Standard text font object |
| `vMenuPane` | `vmenu.h` | Menu bar (pane) |
| `vModalDialog` | `vmodald.h` | Modal dialog box |
| `vPen` | `vpen.h` | Outline pen |
| `vStatusPane` | `vstatusp.h` | Status bar (pane) |

所有 V 类都以小写 `v` 开头。作为一种约定，我从这些类派生自己的类时使用大写 T，表示“Type”。因此在本章中，类 `TCanvasPane` 是从 V 的 `vCanvasPane` 基类派生而来的类。你不必使用我的命名约定，但最好采用一致的风格，以便你能识别自己类的来源。

大多数 V 编程涉及继承类并重写虚函数以响应 X 服务器事件，例如鼠标按钮点击，同时还为你的程序输入和输出提供新函数。刚开始使用 V 时，集中精力确定在何处添加自己的代码。记住要面向对象。让你的类尽可能独立地执行，并让 V 处理与 X 服务器的通信。

### V 欢迎程序

一个简单的程序欢迎你进入 V 编程，并展示了基于类库创建应用程序的最低要求。虽然第 29 章列出了由 V 应用程序生成器创建的程序的各个部分，但本节中的程序（以及本章中的所有其他程序）都是从头开始编写的，使用我自己的 Makefile 和源代码约定。

> **Note**
>
> 本章程序的许多模块具有相同的文件名，因此在编号列表中，这些模块前面加上了其目录名。

本节讨论的 vWelcome 程序分为三个模块：主应用程序、应用程序类和命令窗口类。以下各节描述了这些模块中的每一个，并完整列出了源代码文件。本章中的其他程序在此基础上构建，为节省篇幅未列出重复的编程。始终参考磁盘上的文件以获取完整的源代码。

现在切换到 `src/c30/vwelcome` 目录并输入 `make` 编译程序。然后输入 `./vwelcome` 运行完成的代码文件。图 30.1 显示了程序的窗口。使用鼠标选择 File、Exit 命令关闭窗口并结束程序。对本章中的所有程序都以类似的方式编译、运行和退出。

![](img/6eab91cc30158075ed10d0cabbac9029_763_0.png)

> **Note**
>
> 本章程序的 Makefiles 理解几种选项。输入不带参数的 `make` 来编译并链接所有模块，或者你可以输入 `make all` 做同样的事。输入 `make objs` 仅创建对象文件但不将它们链接到最终的可执行文件。（在大型应用程序中，此选项可能在大量编辑后用于检查语法错误。）要仅编译特定模块，输入其目标代码文件名——例如，输入 `make app.o` 仅编译 `app.cpp` 模块。输入 `make clean` 删除备份、目标代码和完成的执行代码文件，将目录恢复到原始状态。你可能希望在输入 `make clean` 之前将可执行代码文件复制到另一个目录。

#### 主应用程序

vWelcome 的第一个文件包含的编程大致相当于传统 C 或 C++ 程序中的 `main()` 函数。V 应用程序没有 `main()` 函数。相反，如清单 30.2、`welcome.cpp` 所示，V 应用程序构造一个应用程序对象来初始化并运行程序。这使得主应用程序模块相当简单——可以将其视为启动 X 客户端引擎的启动器。

