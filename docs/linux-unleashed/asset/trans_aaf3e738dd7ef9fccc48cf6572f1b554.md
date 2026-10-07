

NE 映像的各个段必须被加载到内存中，并且需要解析对其他 DLL 和 Windows 调用的引用。对外部映像函数的调用通过模块名和函数号来指代。对 `Ellipse` 的调用实际上存储为 `GDI.24`。

可执行映像加载到内存后，Wine 只需跳转到映像中定义的 `WinMain()` 函数即可。对 MS-Windows 图形函数 `Ellipse` 的调用存储为 `GDI.24`。GDI 是 MS-Windows 图形库的名称，而 24 是 `Ellipse` 在该 DLL 中的起始位置。由于 Linux 和 MS-Windows 都使用 i386 指令集，Wine 不需要进行任何指令模拟。当调用 MS-Windows 基元函数时，Wine 会拦截该调用并将其传递给匹配的库例程。

## Wine 库

Wine 将 MS-Windows API 转换为匹配的 X 或 UNIX API 调用。在窗口中绘制椭圆的 MS-Windows `Ellipse` 函数调用具有以下格式：

```
Ellipse(hdc, xLeft, yTop, xRight, yBottom);
```

`xLeft`、`yTop`、`xRight` 和 `yBottom` 的定义是椭圆的包围盒。

同样的椭圆在 X API 的 `XDrawArc` 函数下绘制如下：

```
XDrawArc(display, d, gc, x, y, width, height, angle1, angle2);
```

Wine 需要进行少量数学计算，将 `Ellipse` 调用的坐标转换为 `XDrawArc` 调用的坐标。`XDrawArc` 调用的其他参数映射起来相对容易。*d* 指的是可绘制区域，通常是窗口的句柄。在 MS-Windows 中，这包含在 *hdc* 结构中。*gc* 是图形上下文，在功能上与 MS-Windows 下的 *hdc* 类似。由于 X 能够在网络中的不同机器上显示，*display* 参数描述使用哪个显示器。*display* 参数在 Wine 会话的生命周期内保持不变。Wine 必须考虑的最后一件事是 MS-Windows 的 `Ellipse` 调用还可以指定填充椭圆。Wine 会检查 *hdc*，并可能改用 `XFillArc`。

MS-Windows 下有近 300 个图形基元需要进行类似的转换。虽然这可能看起来工作量很大，但图形转换是 MS-Windows 下较简单的模拟任务之一。

![](img/e8e6b47ac20475e23d48b4c476f5d891_986_0.png)

## Wine 在哪里结束，MS-Windows 从哪里开始？

由于 Wine 目前需要 MS-Windows 的某些部分才能运行，要弄清 Wine 在哪里结束而 MS-Windows 从哪里开始有些令人困惑。Wine 目前为典型 MS-Windows 安装中的以下部分提供 API 调用：

| 模块 | 描述 |
| :--------------------- | :------------------------------- |
| **commdlg** | 常用 Windows 对话框 |
| **gdi** | 图形设备接口 |
| **kernel** | 内核接口 |
| **keyboard** | 键盘接口 |
| **mmsystem** | 多媒体系统接口 |
| **mouse** | 鼠标接口 |
| **shell** | Windows 3.1 Shell API 库 |
| **sound** | Windows 声音系统 |
| **toolhelp** | 调试和工具辅助调用 |
| **user** | 微软 Windows 用户界面 |
| **win87em** | 协处理器/模拟器库 |
| **winsck** | Windows 套接字接口 (TCP/IP) |

Wine 需要访问 MS-Windows 的某些部分以使用 Wine 未实现的功能。一个例子是 MS-Windows 动态链接库 OLECLI，它实现了 OLE 客户端。Wine 团队在减少所需文件数量方面取得了重大进展。Wine 项目章程包括移除对 MS-Windows 文件的任何依赖。这包括用于安装 MS-Windows 应用程序的工具和文件组织结构。

如今，一些最简单的 MS-Windows 应用程序在 Wine 下运行而不需要任何 MS-Windows 代码或访问任何 MS-Windows 目录。WINMINE.EXE 和 SOL.EXE 就是这样的应用程序示例。尽管没有建议的目录结构来支持此操作，但执行此操作的快速示例如下：

-   1. 将 winmine.exe 和 win.ini 复制到 Linux 目录，例如 /users/windows。
-   2. 将 wine.conf 中的 Windows 路径选项更改为 /users/windows，例如。
-   3. 卸载你的 MS-DOS 分区。
-   4. 运行 Wine。

## Wine 的限制

只有少数 MS-Windows 软件包能在 Wine 下正确运行。幸运的是，可以在不实际运行程序的情况下估计程序正常运行的可能性。不幸的是，有一些类型的应用程序很可能永远无法在 Wine 下运行。

## 可用的软件

最新版本的 Wine 支持大量随标准 MS-Windows 3.1 提供的 MS-Windows 小工具和游戏。Wine 的各个版本之间存在相当大的差异。有助于某些应用程序的更改往往会破坏其他应用程序。但在 Wine 下运行相对正常的辅助工具和游戏包括：

-   calc.exe
-   clock.exe
-   cruel.exe
-   golf.exe
-   notepad.exe
-   pipe.exe
-   pegged.exe
-   reversi.exe
-   winmine.exe

## 使用 winestat 分析 Windows 程序

Wine 的一部分是 winestat 实用工具。这实际上是同一个程序作为 Wine，但 winestat 不是运行 MS-Windows 可执行文件，而是仅尝试加载 Windows 可执行文件并报告加载的成功程度。在加载可执行文件时，winstat 还会加载必要的任何 DLL，并报告是否缺少任何 DLL。winstat 查找可执行文件或任何 DLL 使用的 Windows API 调用，并验证它们是否存在。在 MS-Windows 绘图板小工具 pbrush 上运行 winestat 的示例产生以下结果：

```
KERNEL.1 not implemented
KERNEL.54 not implemented
KERNEL.113 not implemented
KERNEL.114 not implemented
KERNEL.121 not implemented
KERNEL.154 not implemented
KERNEL.178 not implemented
KERNEL.207 not implemented
KERNEL: 52 of 66 (86.7%)
USER: 150 of 150 (100.0%)
GDI.151 not implemented
GDI.307 not implemented
GDI.366 not implemented
GDI.439 not implemented
GDI: 80 of 84 (95.2%)
SHELL: 9 of 9 (100.0%)
KEYBOARD: 2 of 2 (100.0%)
TOTAL: 293 of 305 winapi functions implemented (96.1%)
```

winstat 按编号和模块标出 Wine 未实现的各个函数。如果你好奇的是函数名称而不是编号，请查看 Wine 源代码中 `if1632` 目录下给定模块名称的 spec 文件。一个 kernel.spec 文件的示例如下：

```
#1 FATALEXIT
#2 EXITKERNEL
3 pascal GetVersion() GetVersion()
...
...
#54 pascal16 GETINSTANCEDATA
```

.spec 文件中以 # 开头的任何行都被视为注释，而非已实现的函数。在此示例中，1 和 54 都被注释，对应的名称分别为 FATALEXIT 和 GETINSTANCEDATA。FATALEXIT 用于调试错误条件下的 MS-Windows 程序，对大多数 MS-Windows 用户来说并不重要。GETINSTANCEDATA 复制来自应用程序前一个实例的配置数据。如果你只运行一个应用程序实例，这并不适用。

最后的百分比显示了已实现的 MS-Windows API 调用。这通常是衡量应用程序在 Wine 下能正常工作多少的一个良好指标。不幸的是，如果一个未实现的 API 调用对于初始化你的 MS-Windows 应用程序是必需的，那么低于 100% 是不够的。

winstat 给出整体实现评级超过 95% 的 MS-Windows 应用程序值得一试。与 DOSEmu 不同，Wine 不太容易将 Linux 置于不可用状态。然而，终止错误的 Wine 会话并不总是件轻松的事。最简单的做法是使用单独的桌面启动 Wine：`wine -desktop 800x600 filename`。从窗口管理器中终止 Windows 进程的常规方法应该有效。

> **提示**
> 当其他方法都无法停止错误的 Wine 会话时，切换到空闲的虚拟控制台并终止错误的 Wine 进程。例如，Alt+Ctrl 和 F2 将切换到虚拟控制台编号 2。你可以登录到虚拟控制台并使用 `ps -ax | grep wine` 来找到你的 Wine 会话。使用 `kill -15 $pid`，其中 `$pid` 是 `ps` 返回的进程 ID，以停止该进程。
> 你可以通过切换到正在运行 X 的虚拟控制台来返回你的 X 会话。如果你不知道是哪个控制台编号，请按住 Alt 和 Ctrl 键，然后按 F1 到 F8 直到找到它。

## Wine 中缺失的主要部分

Wine 中最明显的缺失可能是缺乏打印机接口。由于这是一个复杂的过程，打印机接口的工作充其量只是几个想法。支持 MS-Windows 下支持的所有类型的打印机将是一项巨大的任务。Wine 很可能只实现一个 PostScript 驱动程序。现有的 Linux 实用程序，如 GhostScript，已经能够将 PostScript 转换为其他类型的打印机类型，例如 HP 激光和喷墨打印机。

32 位 Windows API (win32) 基本上不受支持。这是 Windows NT 和 Windows 95 的可执行映像格式，被称为 PE（可移植执行文件）。Wine 目前支持加载 PE 格式的资源文件（如字体），但无法处理可执行文件或 DLL。

## 不太可能永远可用的软件

Wine 项目没有计划支持 Windows 虚拟设备驱动程序 (VDD)。VDD 使用一种不同的映像格式，称为 LE（线性可执行文件），Wine 加载器无法处理。由于 VDD 执行直接硬件操作等操作，VDD 与 Linux 设备驱动程序共存确实是一个棘手的问题。商用 MS-Windows 中 VDD 的一种用途是 TCP/IP 堆栈。Wine 通过 *winsock* DLL 支持 TCP/IP，该 DLL 使用 Linux 内核固有的 TCP/IP。

## 总结

在本章中，你已经看到如何设置和使用 Wine Windows 模拟器来运行 Windows 应用程序。Wine 不是完成此任务的唯一方法：还有几种其他的 Windows 模拟器和二进制接口可用（例如 WABI）。然而，

