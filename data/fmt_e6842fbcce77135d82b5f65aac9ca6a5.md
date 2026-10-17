
为了说明这些概念，让我们创建一个显示 640x480 顶层窗口的简单应用程序。为了实现这一点，创建两个源文件 `toplevel.h` 和 `toplevel.cpp`，并输入以下代码。

首先是 `toplevel.h`：

```cpp
#ifndef TOPLEVEL_H
#define TOPLEVEL_H

#include "wx/wx.h"

class Toplevel: public wxFrame
{
public:
    Toplevel(const wxString& title,
            const wxPoint& pos = wxDefaultPosition,
            const wxSize& size = wxDefaultSize);
};

#endif
```

以及 `toplevel.cpp`：

```cpp
#include "wx/wx.h"
#include "toplevel.h"

Toplevel::Toplevel(const wxString& title,
  const wxPoint& pos, const wxSize& size)
  : wxFrame(wxFrame *NULL, -1, title, pos, size)

{

}
```

我们在 `Toplevel` 构造函数中所做的是在 C++ 成员初始化列表中调用 `wxFrame` 构造函数。传递给 `wxFrame` 构造函数的参数之前已经定义。

现在定义了 `Toplevel` 类，让我们看看如何使用，查看 `main.cpp` 的源码：

```cpp
#include "wx/wx.h"
#include "toplevel.h"

class MyApp : public wxApp
{
public:
    virtual bool OnInit();
};

IMPLEMENT_APP(MyApp);

bool MyApp::OnInit()
{
    Toplevel *frame = new Toplevel("Hello wxWidgets");
    frame->Show(true);
    return true;
}
```

## wxWidgets

`Show()`（`wxFrame` 继承自 `wxWindow`，`Show()` 在其中定义）会使框架显示。`SetTopWindow()` 是 `wxApp` 的方法，用于告诉 `wxApp` 哪个是应用程序的主窗口。这是一个完全可选的步骤；`wxApp` 将使用顶层窗口作为某些未指定父窗口对话框的父窗口。如果你不指定窗口，`wxApp` 将直接从它维护的列表中为这些目的选择一个窗口。最后，返回 `TRUE` 告诉 `wxApp` 一切顺利；返回 `FALSE` 则会导致应用程序退出。这里是 `main.cpp` 的源代码。

```cpp
#include "wx/wx.h"
#include "toplevel.h"
```

```cpp
class MyApp: public wxApp
{
    virtual bool OnInit();
};
```

```cpp
IMPLEMENT_APP(MyApp)
```

```cpp
bool MyApp::OnInit()
{
    Toplevel *frame = new Toplevel("Toplevel",
    wxPoint(50,50), wxSize(640,480));
    frame->Show(TRUE);
    SetTopWindow(frame);
    return TRUE;
}
```

编译源代码并运行应用程序，将在桌面上显示一个可调整大小的 640x480 窗口。你应该能够调整窗口大小，并通过点击桌面显示的关闭框来关闭它。此应用程序的源代码可以作为你 wxWidgets 应用程序的模板，因为你创建的大多数 wxWidgets 应用程序从根本上都可以基于我们目前为止开发的源代码所示例的结构。

## 添加菜单

让我们继续研究 wxWidgets，为我们的应用程序定义一些需求。通过实现这些新功能，将出现几个额外的 wx 模式。应用程序的新需求如下：

- 主框架应该显示一个带有菜单项的菜单，这些项允许用户退出应用程序并显示“关于”框。
- 主框架应该显示一个实心圆，每当用户调整窗口大小时，该圆都会重绘。

通过实现这些需求，我们将完整开发为框架添加菜单的模式，以及响应之前引入的菜单项选择模式。我们还将讨论管理应用程序绘制的内容以及在窗口中绘制 2D 图形的模式。

### 菜单

让我们从菜单开始。一个菜单由一个或多个菜单项组成。菜单项在被选中时会执行某些操作，而菜单项的名称或标题用于告知选中该项时将执行什么操作。常见的应用程序菜单包括“文件”和“编辑”菜单。“编辑”菜单中的典型菜单项有“剪切”、“复制”、“粘贴”和“撤销”。应用程序菜单通过菜单栏作为一个组显示在窗口顶部。在 OS X 上，桌面上只显示一个菜单栏，对应于当前活动窗口。`wxFrame` 内生支持菜单。要向 `wxFrame` 添加菜单，你必须执行以下操作：

1. 为每个菜单创建一个 `wxMenu` 对象。
2. 将菜单项追加到 `wxMenu` 对象中。
3. 创建一个 `wxMenuBar` 对象。
4. 将每个 `wxMenu` 对象追加到 `wxMenuBar` 对象中。
5. 将 `wxMenuBar` 对象设为 `wxFrame` 对象的活动菜单栏。

让我们过一遍这些步骤。创建 `wxMenu` 对象的代码类似于如下：

```cpp
wxMenu *menuFile = new wxMenu;
```

`wxMenu` 构造函数接受两个参数：标题和样式，但两者都不是必须的，因此我们只需允许默认构造函数被调用。从持有 `wxMenu` 对象指针的变量名 `menuFile` 可以推断出，我们创建的菜单是应用程序的“文件”菜单。你的代码必须为框架菜单栏中的每个菜单创建一个 `wxMenu` 实例。

### wx Widgets

向菜单中追加菜单项只需为菜单中的每个菜单项调用 `wxMenu::Append()` 方法，并向其传递指定菜单项 ID 及其标签的参数。以下代码为“文件”菜单添加了一个“关于”菜单项：

```cpp
menuFile->Append(ID_About, T("&About"));
```

注意标签前的 `&` 字符。紧跟在 `&` 字符后面的字符标识了该菜单项对应的菜单快捷键。

`Append()` 的第一个参数是菜单项的 ID，它在包含该菜单项的框架及其子项中是唯一的。

接下来，我们创建一个菜单栏。通过执行如下代码来实现：

```cpp
wxMenuBar *menuBar = new wxMenuBar;
```

有了菜单栏对象后，我们可以调用它的 `Append()` 函数向其中添加菜单：

```cpp
menuBar->Append(menuFile, T("File"));
```

最后，通过调用 `wxFrameSetMenuBar(menuBar)` 使菜单栏对框架生效：

```cpp
SetMenuBar(menuBar);
```

如果你在此时感到困惑，看到代码中前面的步骤会让一切变得更清晰。以下是到目前的代码：

```cpp
enum
{
    ID_Quit = 1,
    ID_About,
};

Toplevel::Toplevel(const wxString& title,
    const wxPoint& pos, const wxSize& size)
    : wxFrame((wxFrame*)NULL, -1, title, pos, size)
{
    wxMenu *menuFile = new wxMenu;
    menuFile->Append(ID_About, T("&About"));
    menuFile->AppendSeparator();
    menuFile->Append(ID_Quit, T("&Quit"));

    wxMenuBar *menuBar = new wxMenuBar;
    menuBar->Append(menuFile, T("File"));

    SetMenuBar(menuBar);
}
```

## 菜单选择到类函数

现在我们有了应用程序的 UI，需要将菜单选择与代码关联。该策略涉及：

1. 声明事件表并为每个函数添加条目。
2. 实现成员函数。

在头文件 `toplevel.h` 中：在类定义中添加 `DECLARE_EVENT_TABLE()`。为每个选择添加成员函数。这些成员函数的原型如下：

```cpp
#ifndef __TOPLEVEL_H
#define __TOPLEVEL_H

#include "wx.h"

class Toplevel: public wxFrame
{
public:
    Toplevel(const wxString& title, const wxPoint& pos, const wxSize& size);

    void OnQuit(wxCommandEvent& event);
    void OnAbout(wxCommandEvent& event);

    DECLARE_EVENT_TABLE();
};
#endif
```

以下列表显示了 `toplevel.cpp`：

```cpp
#include "wx/wx.h"
#include "toplevel.h"

enum
{
    ID_Quit = 1,
    ID_About,
};

BEGIN_EVENT_TABLE(Toplevel, wxFrame)
EVT_MENU(ID_Quit, Toplevel::OnQuit)
EVT_MENU(ID_About, Toplevel::OnAbout)
END_EVENT_TABLE()

Toplevel::Toplevel(const wxString& title, const wxPoint& pos, const wxSize& size)
    : wxFrame((wxFrame*)NULL, -1, title, pos, size)
{
    wxMenu *menuFile = new wxMenu;
    menuFile->Append(ID_About, T("&About"));
    menuFile->AppendSeparator();
    menuFile->Append(ID_Quit, T("&Quit"));

    wxMenuBar *menuBar = new wxMenuBar;
    menuBar->Append(menuFile, T("File"));

    SetMenuBar(menuBar);
}

void Toplevel::OnQuit(wxCommandEvent& wxUNUSED(event))
{
    Close(TRUE);
}

void Toplevel::OnAbout(wxCommandEvent& wxUNUSED(event))
{
    wxMessageBox(T("Toplevel wxWidgets Sample"),
        T("About Toplevel"),
        wxOK | wxICON_INFORMATION, this);
}
```

## 在框架中绘制内容

显然，目前的 `Toplevel` 应用程序相当无趣且不切实际。在实际应用程序中，框架（Frames）会显示图形数据、控件或这二者的结合。在本节中，我将修改应用程序，使顶层框架显示一个填充的蓝色圆形。当用户调整框架大小时，应用程序将重新绘制该圆，使其能够适应框架的宽度。

任何继承自 `wxWindow` 的控件（包括 `wxFrame`）每当 wxWidgets 认为该控件管理的窗口需要重绘时，都会接收 `wxPaint` 事件。当窗口首次变为可见、当它不再被遮挡（窗口的某部分变得可见，通常是因为它被置于其他窗口之上）以及当它被调整大小时（通过用户或应用程序）时，都会发送 `wxPaint` 事件。对于使用 Win32 的用户，`wxPaint` 事件与 Win32 的 `WM_PAINT` 消息密切相关，并且大部分情况下在相同的情况下发送。

与任何事件一样，安排你的类处理 `wxPaint` 消息涉及两个步骤：

- 1. 在处理 `wxPaint` 事件的类的事件表中添加一个条目。
- 2. 编写 `wxPaint` 事件处理函数。

要在事件表中添加条目，你必须使用 `EVT_PAINT()` 宏。该宏接受一个参数：处理 `wxPaint` 消息的函数名称。在非正式约定中，函数名称通常为 `OnPaint()`。处理程序的函数原型如下：

```
void OnPaint(wxPaint& event)
```

编写 `wxPaint` 消息的处理函数涉及以下步骤：

- 1. 在栈上分配一个 `wxPaintDC` 对象。
- 2. 绘制图形。

`wxPaintDC` 对象封装了之前描述的与平台相关的图形设备上下文（例如 Win32 的 DC 或 X11 的 GC）。应用程序在 `wxPaint` 事件处理程序内部调用 `wxPaintDC` 对象实现的方法，以设置绘制的属性（例如前景颜色或填充颜色），并执行图形操作（例如绘制圆形）。

以下是 `OnPaint` 处理函数的的基本模板：

```
void OnPaint(wxPaintEvent&)
{
    wxPaintDC myDC(this);

    // 设置绘制属性

    // 执行图形操作
}
```

在我们的案例中，我们需要设置的属性是前景颜色（蓝色），图形操作将绘制一个适应框架窗口宽度的圆形。以下 `TopLevel::OnPaint()` 的实现实现了这些目标。列表如下：

```
void TopLevel::OnPaint(wxPaintEvent&)
{
    int width, height;
    wxBrush brush(wxColour(0,0,255), wxSOLID);

    wxPaintDC myDC(this);
    myDC.SetBrush(brush);

    GetClientSize(&width, &height);

    myDC.DrawCircle(width >> 1, height >> 1, width >> 1);
}
```

`wxBrush` 对象正如你预期的那样，会创建一个画笔，定义了在 wxWidgets 中绘制矩形、圆形和其他凸多边形 2D 图形时使用的填充颜色和样式。画笔可以是实色的、透明的、网格的或点纹的（可以提供点阵位图作为 `wxBrush` 构造函数之一的参数）。我在这里使用的构造函数接受 `wxColour` 对象的引用，该对象在此处初始化为 RGB 三元组红=0、绿=0、蓝=255，以及一个样式参数，设置为 `wxSOLID`。然后使用 `wxDC::SetBrush()` 方法将此画笔与设备上下文关联，这样当我们绘制圆形（通过调用 `wxDC::DrawCircle()`）时，它将被填充为实蓝色。`wxDC::DrawCircle()` 的参数是圆心的 x 和 y 坐标以及圆的半径。我们使用 `wxWindow::GetClientSize()` 方法（记住 `wxFrame` 继承自 `wxWindow`）来确定 `wxFrame` 管理的窗口客户区域的宽度和高度，如你所见，这些值被用于计算 `wxDC::DrawCircle()` 的 x、y 和半径参数。`GetClientSize()` 返回客户区域的尺寸，即不包含框架顶部菜单栏或底部状态栏（如果存在的话）的窗口区域。

最后，要做的工作就是将 `OnPaint()` 添加到 `Toplevel` 事件表中。这可以通过在 `BEGIN_EVENT_TABLE()` 和 `END_EVENT_TABLE()` 宏之间添加以下行来实现：

```
EVT_PAINT(Toplevel::OnPaint)
```

## 提高 OnPaint 处理程序的质量

对于经验丰富的图形程序员来说，像在 `OnPaint()` 中那样直接向窗口绘制图形被认为是不理想的，特别是在图形复杂或绘制耗时较长的情况下。这是因为以这种方式向窗口绘制会导致明显的闪烁。

一种经常用于克服闪烁的策略是重构如 `OnPaint()` 类的函数，使其将其图形绘制到离屏缓冲区而不是直接绘制到窗口上。当绘制完成后，`OnPaint()` 将离屏内存的内容直接拷贝到窗口，并在那里进行显示。因为将离屏内存拷贝到窗口的时间极快，对窗口进行的更改会立即出现。

绘制离屏内容涉及以下简单步骤：

- 1. 创建一个离屏内存 DC。
- 2. 使用内存 DC 绘制图形。
- 3. 将内存 DC 的拷贝（Blit）到窗口。

创建内存 DC 是轻而的，可以通过实例化 `wxMemoryDC` 类来实现，如下：

```
wxMemoryDC dc;
```

`wxMemoryDC` 继承自 `wxDC`，与 `wxPaintDC` 相同可以针对 `wxDC` 调用的方法，例如 `SetBrush()` 和 `DrawRectangle()`。在图形已绘制到内存 DC 后，从内存 DC 传输到窗口是通过调用 `wxPaintDC` 的 `Blit()` 方法实现的。`Blit()` 的函数原型如下：

```
bool Blit(wxCoord xdest, wxCoord ydest, int width, int height, wxDC* dc, wxCoord xsrc, wxCoord ysrc, int logicalFunc);
```

对于我们的目的，我们只需要将源 DC 的所有位拷贝到目标 DC，因此我们传递 `wxCopy`。这是我们对 `Blit()` 的调用：

```
myDC.Blit(0, 0, width, height, &memdc, 0, 0, wxCopy);
```

传递给 `Blit()` 的第一个参数指定了源 DC 中的拷贝区域，第五参数指定了目标 DC 中的拷贝起点，最后的参数告诉 `Blit()` 直接拷贝像素。
