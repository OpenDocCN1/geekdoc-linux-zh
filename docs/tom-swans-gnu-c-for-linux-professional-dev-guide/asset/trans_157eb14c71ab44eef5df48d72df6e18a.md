

## WINDOW CANVAS

窗口的大部分视觉活动都是通过在窗口画布上绘制图形和文本来处理的。为此，应用程序会创建一个派生自 V 提供的多个类之一的窗口画布对象。

在示例生成的应用程序中，主窗口的画布对象属于名为 myCanvasPane 的类，该类派生自 vCanvasPane 基类。清单 29.5 显示了该类的声明（此处已编辑以便正式查看）。

### LISTING 29.5 MYCVN.H (PARTIAL)

```
#include <v/vcanvas.h>

class myCanvasPane : public vCanvasPane {
public:
    myCanvasPane();
    virtual ~myCanvasPane();

    // Scrolling
    virtual void HPage(int shown, int top);
    virtual void VPage(int shown, int top);
    virtual void HScroll(int step);
    virtual void VScroll(int step);

    // Events
    virtual void MouseDown(int x, int y, int button);
    virtual void MouseUp(int x, int y, int button);
    virtual void MouseMove(int x, int y, int button);
    virtual void Redraw(int x, int y, int width, int height);
    virtual void Resize(int newW, int newH);
    ...
};
```

myCanvasPane 类声明了通常的构造函数和析构函数，以及一些用于滚动和处理输入输出事件的成员函数。要响应用户在窗口画布区域内单击鼠标，只需重写 MouseDown() 函数并提供所需的编程即可。

图形处理方式类似。要在窗口中绘制图形，请重写 Redraw() 并调用所需的图形输出函数（更多内容见第 30 章）。此时不必担心如何绘制实际对象。只需注意 Redraw() 是为特定窗口添加此代码的位置。它相当于 Xlib 程序对 Expose 事件的响应。如果窗口需要重绘——例如用户移动另一个窗口使其暴露时——V 会按需调用 Redraw() 来更新窗口的画布。四个参数表示需要重绘的窗口部分，但除非是高度复杂的图形，否则您可以简单地绘制全部内容并忽略这些值。Resize() 函数对应于 Xlib 的 ConfigureNotify 事件。

## MODAL AND MODELESS DIALOG BOXES

生成的 V 应用程序其余的主文件实现了程序的示例模态和非模态对话框。创建这些对象超出了本介绍的范围。然而，您可能希望查看相关文件：mydlg.h、mydlg.cpp、mymdlg.h 和 mymdlg.cpp。

浏览这些文件时，请注意使用了静态结构来定义对话框按钮、标签和其他项目。正如您可能猜到的，对话框只是专门化的窗口对象，它们的工作方式与前面描述的命令窗口非常相似。例如，每个都有一个 DialogCommand() 函数，它与 WindowCommand() 类似，用于响应用户输入——例如单击按钮。要编程一个对话框，您只需从 VDialog 或 VModalDialog 基类派生一个类，提供静态结构来定义对话框的组件，并在构造函数中初始化该对象。然后重写 DialogCommand() 以响应用户输入。

## SUMMARY

V 是一个类库，大大简化了 V 应用程序的开发。V 在 GNU 通用公共许可证下自由分发，完全面向对象。它也与 Microsoft Windows 和 OS/2 兼容。如果您使用 V for X 编写了一个应用程序，您只需使用 Borland C++ 或 Watcom C++ 等合适的开发系统重新编译它即可在 Microsoft Windows 下运行。

有关本章介绍主题的更多信息，请参阅以下章节：

- Chapter 26, “Introducing X Programming”
- Chapter 30, “Developing X Software with V”

## CHAPTER 30

## Developing X Software with V

第 29 章介绍了用于 X 编程的 V 类库。本章将引导您了解大多数 X 客户端应用程序所需的一些基本技术，并展示您如何使用 V 为 Linux 和其他受支持的操作系统开发完成的 X 软件。阅读本章后，您应该能够更好地理解 V 的在线教程和参考资料，并且也能够阅读和理解随库提供的示例程序。

## COMPILING THIS CHAPTER'S PROGRAMS

本章的程序分为单独的模块，因此它们分别存储在子目录中。要编译本章的程序，请更改到指定的目录（例如 src/c30/welcome）并输入 make。如果收到错误，请编辑 src/c30 目录中的 Config.mk 文件，并在清单 30.1 中显示。

```
LISTING 30.1 CONFIG.MK
# Edit the following for your installation (esp HOMEV)
CC = g++
HOMEV = $(HOME)/v
VIncDir = $(HOMEV)/include
VLibDir = $(HOMEV)/lib
X11INC = /usr/X11R6/include
X11LIB = /usr/X11R6/lib
LIBS = -lVx -lXaw -lXmu -lXt -lXext -lX11
# ===========================================
# Compiler and linker flags
CFLAGS = -O -I$(X11INC) -I$(VIncDir)
LFLAGS = -O -L$(X11LIB) -L$(VLibDir)
```

如果需要，请更改 HOMEV 为您根据第 29 章所述安装 V 的目录。默认情况下，Config.mk 使用为您的 shell 定义的 HOME 环境变量。大多数读者无需对此处列出的文件做很少或根本不需要的更改。

> Note
> 如果您已安装了较早版本的 V，您可能需要将 LIBS 设置中的 -lVx 改为 -lV，并将 VLibDir 设置为 /lib/linux。其他设置应按此处所示工作。为了获得最佳效果，您应安装本书记载的 CD-ROM 上提供的 V 的新版本，该版本也可通过互联网获得，详情见第 29 章“Introducing the V Class Library。”

## UNDERSTANDING V CLASSES

V 的在线文档附带了绘制精美的图表，说明了库的类层次结构。我怀疑我无法改进这些图表，因此与其在此重复它们，表 30.1 列出了 V 的主要类以及它们被声明的头文件。这绝不是一个完整的列表，但显示了应用程序中最常使用的类和头文件

