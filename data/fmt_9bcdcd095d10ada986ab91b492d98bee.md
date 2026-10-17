
```
/*
 * spreadkey.c - 简单的基于 S-Lang
 */
#include <stdio.h>
#include <string.h>
#include <slang/slang.h>

int main(int argc, char *argv[])
{
    int i = 0;
    unsigned int ch;

    /* 初始化 lang */
    initscr();

    /* 绘制一个边框 */
    box(stscr, ACS_VLINE, ACS_HLINE);
    mvaddstr(stscr, 1, 1, "INPUT:");
    refresh();

    /* 读取字符直到遇到换行符 */
    noecho();
    while (1) {
        ch = getch();
        if (ch == '\n') {
            break;
        }
        ++i;
        getx(stscr, y, x);
        /* 在右侧边缘 */
        if (x == 79) {
            mvaddch(y + 1, 1, ch);
        } else {
            waddch(stscr, ch);
        }
    }

    refresh();
    echocho();
    refresh();

    /* 打印字符计数 */
    getmaxx(stscr, maxx, maxy);
    mvprintw(stscr, maxy - 2, 1, "characters read: %d\n", i);
    curs_set(0);
    refresh();

    /* 观察屏幕的时间 */
    sleep(3);

    /* 退出 lang */
    endwin();

    return 0;
}
```

要编译此程序使用以下命令：

```
$ gcc sreadkey -lslang -o sreadkey
```

编译和运行此程序需要 `slang`, `slang-dev`, `ncurses` 和 `ncurses-devel` 包。

要运行程序，输入 `./sreadkey`。图 29-8 显示了输入与早之前 `readme.c` 相同文本后的结果。

# 图 29-8

一个基于 S-Lang 的 TUI

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_808_0.png)

基于 S-Lang 的程序也可以从 `stdin` 管道读取输入。

从开发者的角度来看，`ncurses` 和 S-Lang 在程序结构和实际用法上有很大，但输出几乎相同。

> 注意
> 有关 S-Lang 的更多信息（包括下载信息），请访问 S-Lang 网页 `www.s-lang.org`。

# 创建图形界面

在创建 GUI 时，Linux 程序员拥有的比创建 TUI 更多的选项。最流行且广为人知的创建图形应用程序的工具包是 `Qt` 和 `GTK+`。`Qt` 是 C++ 框架，带来了 KDE 桌面环境。`GTK+` 是 GNOME 桌面环境底层的工具包。`GTK+` 主要用 C 编写，但它支持许多其他编程语言（如 Perl、C++ 和 Python），因此你可以在许多编程环境中使用 `GTK+` 功能。由于可用空间有限，本章没有显示 `Qt` 和 `GTK+` 的示例。

# 第六部分：在 Linux 中编程

## 注意事项

关于 `GTK+` 的更多信息，请访问 `GTK+` 网站 `www.gtk.org`。你可以在 `http://qtsoftware.com/` 找到有关 `Qt` 框架的信息。

尽管 `Qt` 和 `GTK+` 是 Linux 图形界面开发的主力工具，但你可以使用许多其他工具、框架和库来为 Linux 开发基于 GUI 的应用程序。以下列表按字母顺序排列，描述了一些可用的工具包。大多数工具包和框架都描述了部件集（widget sets），这些部件集在一个或多个编程库中实现。“部件”（Widget）是用于用户界面抽象的术语，例如使用工具包创建的滚动条或按钮。

> 注意
> 列表列出的每个程序在本书包含的各种 Linux 发行版（Fedora, Ubuntu, openUSE, Debian 等）中均可用。请使用合适的软件包工具来查找并安装你感兴趣的编程工具。

- Athena — Athena 库是 Window 系统最早可用的（可以认为是古老董董的）部件库之一。它是原始 Xib 调用之上的抽象层，使得创建滚动条、文本输入框和其他 UI 元素变得稍微容易了一些。它是标准 X11 分发的一部分。

- 3D Athena — 3D Athena 工具包是原始 Athena 工具包的 3D 版本。它赋予了 Athena 外观，并且比原生的 Athena 有了显著改进。3D Athena 工具包虽然不再被广泛使用，但在网页上 `http://directory.fsf/zaw3d` 仍然可用。

- FLTK — FLTK 读音为“full tick”，是 Fast Light Toolkit（快速轻量工具包）的缩写。FLTK 是一个用于 X、Mac OS 和 Microsoft Windows 的 GUI。FLTK 使用 C++ 编写，使得编写出无论 GUI 运行在何种平台上，外观看起来几乎完全相同的 GUI 成为可能。FLTK 还支持 OpenGL 图形。你可以在网页上 `www.fltk.org` 找到更多关于 FLTK 的信息。

- XForms — XForms 是构建在 Xlib 之上的 GUI。它不像本节讨论的其他 GUI 工具包那样高度可配置，但它的简单性使得 XForms 比其他图形工具包更容易使用。它带有一个 GUI 构建器，可以轻松地获取工作并运行应用程序。关于 XForms 的更多信息可以在网页 `http://savannah.nongnu/projects/xforms/` 上找到。

- OpenGL — OpenGL 是行业标准的 3D 图形工具包。它为 X Window 系统提供了目前最真实且栩生生的图形。它通常作为 Free86 的一部分提供。关于 OpenGL 的更多信息可以在网页 `www.opengl.org` 上获得。

- Motif — Motif 是 X Window 系统最早的接口工具包之一，它结合了接口工具包和窗口管理器。最初作为商业产品提供，现在以开源版本 OpenMotif 的形式从 `www.openmotif.org` 的 Motif 提供。

### 第 29 章：编程环境与接口

- `Xlib` — X 库的缩写，是用于原始 X Window 系统协议的低级、基于 C 语言接口。如果你希望编写尽可能接近 X 图形的代码，请编写基于 `Xlib` 的程序。事实上，窗口管理器、部件库和 GUI 工具包都是使用 `Xlib` 函数编写的。虽然使用 `Xlib` 可以让你获得性能，但它的代码量非常庞大。`Xlib` 是标准 X 分发中的核心要素。你可以从网页 `http://www.tronche.org/gui/x/xlib` 上的 HTML 手册学习更多关于 `Xlib` 的知识。

- `Xt` — 内部属性（Intrinsics）是 `Xlib` 之上层非常薄的函数和数据结构。`Xt` 内部属性创建了一个面向对象的接口，C 程序可以使用它来创建图形元素。如果没有其他部件，这些内部属性并没有特别有用。`Xt` 和 `Xlib` 一样，是标准 X 分发的一部分，不单独提供。

# 应用程序编程接口

应用程序接口（或 API）为编程人员提供了用于执行特定任务的代码库。API 有很多，其数量可能与需要解决的编程问题类型一样。例如，`ncurses` 库提供了一个用于创建文本用户界面的 API。反之，`ncurses` 通过使用 `terminfo` 或 `termcap` API 以与正在使用的设备一致的方式执行实际的屏幕更新。

开发者不断需要执行特定类型的编程任务，例如更新数据库、通过网络通信、从声卡输出声音或进行数学计算。因此，至少存在一个数据库 API、socket API、声音 API 或数学 API 可供他们使用以简化这些任务。

> 注意
> 本节讨论了用于 C 和 C++ 编程的 API。你也可以在其他编程语言中使用这些库，但你可能需要编写软件来适配基于 C 的 API。例如，Perl、Python 和 Java 都有调用 C 函数或 API 的方法，但你将需要编写代码将实际的 C 库适配到你的编程语言。

API 由三个部分组成：

- **头文件** — 声明开发者可以在自己的程序中使用的接口（函数调用、宏和数据结构）。

- **一个或多个库文件** — 头文件中声明的接口的实现，程序必须与这些文件进行链接。

- **API 文档** — 描述如何使用 API，并通常提供示例代码。文档可能以手册页（manual pages）、文本文件、HTML 文件、GNU TeXinfo 文件或这些格式的某种组合提供。

表 29-1 描述了许多流行或广泛使用的 API，但此处提供的列表并不完整。

| API | 类别 | 描述 |
| --- | --- | --- |
