
```
	if(*timer) KillTimer( hParent, (*timer));

}

}
```

以下示例显示了使用 WM_TIMER 的 Win32 定时器：

```c
#define timer1 1
#define timer2 2

LRESULT WndProc( HWND hwnd,
	UINT message,
	WPARAM wParam,
	LPARAM lParam)
{
	switch (message) {
	case WM_CREATE :

	//+
	// 创建两个定时器
	//-
	SetTimer( hwnd, timer1, 1000, (TIMERPROC) NULL );
	SetTimer( hwnd, timer2, 1000, (TIMERPROC) NULL );
	break;

case WM_TIMER:

//+
// wParam 指定定时器标识符
// 如果处理了此消息则返回零 (0)
//-
switch (wParam) {
case timer1 :
// 执行定时器任务
break;
case timer2 :
// 执行定时器任务
break;
default:
break;
}
return ( FALSE );

case WM_DESTROY :
//+
// 停止两个定时器
//-
KillTimer( hwnd, timer1 );
KillTimer( hwnd, timer2 );

PostQuitMessage(0);
break;
```}

## 迁移基于字符的接口

并不是所有基于 UNIX 的接口都是图形化的。在工作站出现之前，基于字符的接口是 UNIX 计算的主流。基于字符的接口有两种选择：可以以极小的更改迁移到 POSIX 环境，或者使用基于图形的接口替换基于字符的接口。

### POSIX 终端 I/O

POSIX `termios` 结构和一组新的访问调用取代了传统的终端接口，即 System V 中的 `termios` 结构和 BSD 中的 `stty` 结构。POSIX 输入输出（I/O）模型与 System V 非常相似。存在两种模式：规范（canonical）和非规范（noncanonical）。规范输入是基于行的，如 cooked 模式；非规范模式是基于字符的，如 raw 或 cbreak 模式。POSIX 子系统包含真正的非规范模式，支持 `cc_MIN` 和 `cc_TIME`。

`termios` 结构定义在 `termios.h` 中，如下：

```c
struct termios {
    tcflag_t c_iflag;      /* 输入模式 */
    tcflag_t c_oflag;      /* 输出模式 */
    tcflag_t c_cflag;      /* 控制模式 */
    tcflag_t c_local;      /* 本地模式 */
    speed_t c_ispeed;      /* 输入速度 */
    speed_t c_ospeed;      /* 输出速度 */
    cc_t c_cc;             /* 控制字符 */
};
```

POSIX SDK 扩展了 `c_iflag` 的 POSIX 标志集，包含了 `IXON` 和 `IREAD`。对于 `c_cc`，`MIN` 和 `TIME` 的值与 EOF 和 EOL 不同。然而，对于可移植应用程序，开发者应该考虑到在 POSIX 系统上 MIN 和 TIME 不能等同于 EOF 和 EOL。

表 11.8 显示了取代终端 I/O `ioctl()` 的函数，包括 `ioctl(fd, TIOCSETP, buf)` 和 `ioctl(fd, TIOCGETP, buf)` 或 `stty()` 和 `getty()`。之所以进行更改是因为最后一个参数的数据类型导致无法进行检查。

#### 表 11.8. 取代终端 I/O ioctl() 的函数

| 函数 | 说明 |
| :--- | :--- |
| `tcgetattr()` | 获取属性（termios 结构）。 |
| `tcsetattr()` | 设置属性（termios 结构）。 |
| `cfgetispeed()` | 获取输入速度。 |
| `cfgetospeed()` | 获取输出速度。 |
| `cfsetispeed()` | 设置输入速度。 |
| `cfetspeed()` | 设置输出速度。 |
| `tcdrain()` | 等待所有输出传输完毕。 |
| 函数 | 说明 |
| :--- | :--- |
| `tcflow()` | 暂停发送或接收。 |
| `tcflush()` | 刷新挂起的 I/O。 |
| `tcbreak()` | 发送 BREAK 字符。 |
| `tcgetpgrp()` | 获取前进程组标识符 (ID)。 |
| `tcsetpgrp()` | 设置前进程组 ID。 |

要获取窗口大小，可以使用 `ioctl(0)` 的 `TIOCGWINSZ` 命令或 `winsize` 结构，这者都支持。

### 将 curses 和终端函数迁移到 Interix

Interix SDK 库包括 `Libcurses.a`（ncurses 包的移植版）和 `Libtermcap.a`（termcap 函数）。Interix SDK 还支持伪终端。将这些应用程序迁移到 Interix 应该是简单的，但请注意以下点：

- curses 函数频繁使用存储在 `/usr/share/terminfo` 的 terminfo 数据库。该位置与传统系统使用的位置不同。要链接 terminfo 运行时，请链接 `curses` 库。
- Interix 同时支持 BSD 的 `/dev/ptypnn` 和 System V 的 `/dev/ptmx` 方法来打开伪终端的主端。System V 方法稍快，因为对可用设备的搜索是在子系统中处理的。目前，Interix 子系统在主端支持 265 个名为 `/dev/pty[p-zA-E]-[0-9a-f]` 的 pty。相应的从设备命名为 `/dev/tty[p-zA-E]-[0-9a-f]`。
- 当使用 `/dev/pty` 时，可以使用 `psname()` 获取从（从）tty 名称。基于 BSD 的 `ioctl(1)` 调用可用于 pty 主端。
- 只要是会话首进程，进程在第一次调用 `open()` 打开 tty 时不会获取控制终端，除非在 `open()` 调用中指定了 `NOCTTY`。

## 移植 OpenGL

OpenGL 最初由 Silicon Graphics 开发，是一组与平台无关的图形 API。这使得 OpenGL 对于想要针对多个平台的开发者来说是一个极具吸引力的选择。将图形应用程序从一个平台迁移到另一个平台时，几乎不需要（如果完全不需要）特定平台的代码。OpenGL 扩展允许对特定平台的代码进行隔离和处理。

然而，OpenGL 并不是一套窗口库。带有窗口的 OpenGL 应用程序使用目标平台的窗口系统（X Windows 或 Win32）、`(GLUT)` 或跨平台库，如 OpenGL 图形库实用工具包（OpenGL Graphics Library Utility Kit）。但是，由于许可方面的考虑，大多数商业应用程序都包含了目标平台的窗口系统。因此，当把使用 OpenGL 的 UNIX 应用程序迁移到 Windows 时，其迁移考虑因素可能与非 UNIX 应用程序相似。本节的剩余部分涵盖了 OpenGL 应用程序迁移的额外 GUI 考虑因素。

除了窗口系统本身，OpenGL 应用程序还需要到主窗口系统的“上下文”（context）。目前已开发了一套用于窗口上下文的特殊 OpenGL 扩展。UNIX 应用程序通常用于 X Windows 的 GLX OpenGL 扩展。基于 Windows 的应用程序通常使用 WGL (wiggle) OpenGL 扩展。在任何情况下，都需要这三个主要函数：

- 创建上下文
  - X Windows: `glXCreateContext`
  - Win32: `wglCreateContext`
- 使上下文成为当前
  - X Windows: `glXMakeCurrent`
  - Win32: `wglMakeCurrent`
- 删除上下文
  - X Windows: `glXDeleteContext`
  - Win32: `wglDeleteContext`

如果在迁移后应用程序仍然需要支持 UNIX，可以使用 C/C++ 预编译器指令 (`#ifdef`) 来针对适当的平台。

OpenGL API 在 UNIX 和 Windows 上都是 C 语言库。Fortran 应用程序也可以使用 OpenGL。为了让 Fortran 应用程序更容易使用 OpenGL，通常存在一个 Fortran 90 模块来处理 Fortran 和 C 调用约定之间的转换。Windows 上的绝大多数 Fortran 编译器都为 OpenGL 提供了一个可选的 Fortran 模块。

## 第 11 章迁移用户界面

有关 OpenGL 和特定平台示例的更多信息，请参阅 SGI OpenGL 网站 (`http://www.sgi.com/software/opengl/`) 或 opengl.org 网站 (`http://www.opengl.org/`)。

### GDI+

GDI+ 是一个为 C/C++ 程序员设计的基于类的 API。它允许应用程序在视频显示器和打印机上使用图形和格式文本。基于 Windows 的应用程序不直接访问图形硬件。相反，GDI+ 代表应用程序与设备驱动程序交互。64 位 Windows 操作系统也支持 GDI+。

要使用 GDI+，开发者必须将 `Gdiplus.dll` 库复制到用户计算机的系统目录。有关使用特定类或方法需要哪些操作系统的信息，请参阅该类或方法文档中的“要求”部分。

所有基于 Windows 的应用程序都可以使用 GDI+，这是 Windows XP 和 Windows .NET Server 操作系统中的一项新技术。它适用于运行在 Windows NT 4.0 SP6、Windows 2000、Windows 98 和 Windows Millennium 版操作系统上的应用程序。

要下载最新的可发行包，请访问 `http://www.microsoft.com/download/platformsdk/sdkupdate/psdkredist.htm`。

### 将 X Windows 术语映射到 Microsoft Windows

UNIX 和 Microsoft Windows 的图形模型非常不同。它们存在概念上的相似之处，但几乎无法进行并行映射。本节将尽可能描述这些联系。

在本节的标题中，Win32 GDI 术语将以以下格式跟随对应的 X Windows 术语：

X Windows 对比 Win32 术语

#### 回调 (Callback) 与 WindowProc

Win32 使用 `WindowProc` 函数的作用与 X Windows 中的 Callback 相同。一个 X 组件可以关联一个回调列表，但 Win32 窗口只有一个入口点来处理发送给它的消息。

#### 客户端 (Client) 与 客户端窗口 (Client Window)

X Windows 由一个描述客户端如何与运行在远程计算机上的服务器交互的协议组成。对象的绘制是由服务器负责。这为客户端应用程序提供了设备独立性，因为它不需要了解任何关于物理硬件的知识。

在 Microsoft Windows 环境中，图形设备接口 (GDI) API 提供了这种设备独立层。基于 Windows 的应用程序像 X 客户端一样，不需要直接访问图形硬件。GDI 通过代表应用程序使用设备驱动程序与硬件交互。

单个基于 Windows 的应用程序可以包含许多个独立的窗口。每个窗口都可以有窗口框、标题栏、系统菜单、最小化和最大化按钮，但它有一个主显示区域，被称为客户端窗口。

Windows 多文档界面 (MDI) 应用程序有三种窗口：框架窗口、MDI 客户端和若干子窗口。在这种情况下，“客户端窗口”一词具有特殊含义。关于 MDI 的更多信息，请参阅 MSDN 网站上的 MDI 文档 (`http://msdn.microsoft.com/`) 或 Platform SDK。

#### 控制台模式 (Console Mode) 与 命令窗口 (Command Window)

如果 X Windows 或或其他图形用户界面没有运行在 UNIX 系统上，用户必须在纯文本模式或*控制台模式*下工作。

将 Microsoft Windows 想为完全相反的。如果没有运行控制台，用户必须在 GUI 模式下工作。

#### DPI 与 屏幕分辨率

在启动 X Windows 会话时，使用 `dpi` 选项可以提高大分辨率显示器（如 1600x1200）上的外观。基于 Windows 的应用程序在构建时通常对其运行系统的能力不做任何假设。系统 API 用于计算缩放和其他特性。`GetDeviceCaps()` 用于获取系统的 DPI。

#### 图形上下文 (Graphics Context) 与 设备上下文 (Device Context)

X Windows 图形上下文 (GC) 包含了关于如何执行绘制所需的信息。Win32 设备上下文 (DC) 提供类似的信息。各自使用的函数总结在表 11.9 中。

##### 表 11.9 X Windows GC 与 Win32 DC 可比较函数

| Xlib | Win32 |
|---|---|
| `XtGC` | `GetDC` |
| `XtReleaseGC` | `ReleaseDC` |
| `XCreateGC` | `CreateDC` |
| `XFreeGC` | `DeleteDC` |

#### 资源 (Resources) 与 属性 (Properties)

在 X Windows 术语中，组件由其资源定义。宽度、高度、颜色和字体都是资源的示例。可以使用 `VaCreateManagedWidget()` 管理资源，或者通过资源文件或 `VaGetValues()`。

在 Win32 术语中，控件由其属性定义。例如文本控件具有以下属性：垂直居中、不换行、透明、右对齐、可见。

#### 资源文件 与 注册表

X Windows 使用称为资源的文件来存储有关特定 X Windows 客户端的系统设置或偏好的信息。

在基于 Windows 的系统中，这类信息存储在注册表中。注册表以分层树形结构存储数据。有一个包含 40 多函数的 Win32 API 帮助访问注册表。如需更多信息，请在 MSDN 网站上搜索“注册表”或“注册表函数”。

文件的扩展名为 `.rc`，并包含一种特殊的资源语言（脚本），该脚本由资源编译器进行编译。生成的文件 (`.res`) 会与包含它的应用程序链接。

欲需更多信息，请在 MSDN 网站（`http://msdn.microsoft.com/`）上搜索“using resources”（使用资源）。

### 根窗口 vs. 桌面窗口

所有的 X 窗口都是根窗口（root window）的后代。在 Windows 环境中，桌面窗口是一个系统定义的窗口，所有应用程序显示的窗口的基础。

### /bin vs. System32

在 Windows 中，`/System32` 目录大致相当于 UNIX 系统上的 `/bin` 目录。系统可执行文件位于此处。`/System32` 目录位于系统根目录。要找到系统根目录，在命令提示符中输入 `set` 并回车。这将显示当前的环境列表。在列表中找到 `SYSTEMROOT`。在 `SYSTEMROOT` 下，有一个类似于 `SYSTEMROOT=C:\WINNT` 的项。这就是系统目录，而该目录下就是 `/System32` 目录。

### /usr/bin vs. Program Files

Windows 系统上的 `Program Files` 目录类似于 UNIX 系统上的 `/usr/bin` 目录。这是用户应用程序的默认位置。在 Windows 中，用户可以创建多个此类目录。例如，每个驱动器都可能有一个 `Program Files` 目录。系统环境变量 `ProgramFiles` 包含一个默认位置的路径，例如 `ProgramFiles=C:\ProgramFiles`。

### /usr/lib vs. LIB 环境变量

在 Windows 中，用户库的路径可以在任何地方。为了管理这种关系，请获取或设置系统环境变量 `LIB`。

### /usr/include vs. INCLUDE 环境变量

在 Windows 中，用户包含文件的路径可以在任何地方。为了管理这种关系，请获取或设置系统环境变量 `INCLUDE`。

### Pixmap 或 Bitmap vs. Bitmap

在 X Windows 中，bitmap 和 pixmap 的用法与 Win32 位图（bitmap）相同。例如，它们可以作为图片、填充图案、图标和光标。然而，它们在形式上非常不同。

下面的 X Windows 示例表示了一个简单的 16x16 “X”字形：

```c
#define simple_width 16
#define simple_height 16
static unsigned char simple_bits[] = {
0x01, 0x80, 0x02, 0x04, 0x20, 0x20, 0x08, 0x10, 0x10, 0x08, 0x20, 0x20, 0x04,
0x40, 0x02, 0x80, 0x01, 0x80, 0x01, 0x02, 0x20, 0x04, 0x10, 0x08,
0x08, 0x10, 0x04, 0x20, 0x02, 0x40, 0x01, 0x80
};
```

下面的 Win32 示例也表示了一个简单的 16x16 “X”字形：

| 00000 | 42 | 7E | 00 | 00 | 00 | 00 | 00 | 00 | 3E | 00 | 00 | 28 | 00 |
| 000010 | 00 | 10 | 00 | 00 | 10 | 00 | 00 | 00 | 01 | 00 | 00 | 00 | 00 |
