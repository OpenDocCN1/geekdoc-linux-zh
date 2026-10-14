

## LISTING 30.6 VWELCOME/CMDWIN.CPP

```cpp
#include "cmdwin.h"
#include <v/v_defs.h>  // Need standard definitions

// Define a simple menu command item
static vMenu FileMenu[] =
{
  {"&Exit", M_Exit, isSens, notChk, noKeyLbl, noKey, noSub},
  {NULL}
};

// Define a simple top-level menu item
static vMenu StandardMenu[] =
{
  {"&File", M_File, isSens, notUsed, notUsed, noKey,
   &FileMenu[0]},
  {NULL}
};

// Our command window constructor
TCmdWindow::TCmdWindow(char* name, int width, int height) :
  vCmdWindow(name, width, height)  // Call ancestor constructor
{
  myMenu = new vMenuPane(StandardMenu);  // Create menu pane
  AddPane(myMenu);                        // Add it to our window
  myCanvas = new vCanvasPane;             // Create window canvas
  AddPane(myCanvas);                      // Add it to our window
  ShowWindow();                           // Make window visible
}

// Our command window destructor
TCmdWindow::~TCmdWindow()
{
  delete myMenu;  // One for each "new" in constructor
  delete myCanvas;
}

// Respond to menu selections and other commands
void TCmdWindow::WindowCommand(
  ItemVal id, ItemVal val, CmdType cType)
{
  switch (id) {
  case M_Exit:      // User selected File\Exit command
    theApp->Exit(); // Exit the application
    break;
  default:          // Route unhandled commands
    vCmdWindow::WindowCommand(id, val, cType);
    break;
  }
}
```

TCmdWindow 类的实现是其中最大的，而且对于大多数 V 应用程序来说，这一点可能都是正确的。前两项是常见的 C++ 结构体声明，它们创建了程序下拉菜单栏的字符串和其他选项。V 对菜单、工具栏、状态栏和对话框使用类似的结构。这与一些其他 X（以及 Microsoft Windows）开发系统不同，后者依赖资源来处理这类项目。在 V 中，你在程序的源代码文件中创建所有程序元素。本章的其他部分更详细地解释了这些结构，所以我在这里就不展开了。

模块中接下来是 TCmdWindow 构造函数和析构函数。构造函数有两个重要职责——为类的私有数据成员指针创建对象，并调用一个使窗口可见的 ShowWindow() 函数。窗口构造函数还可能执行其他操作——例如，初始化一个容器对象来存储有关程序窗口的信息。（下一节将详细介绍。）

TCmdWindow 析构函数应执行与此窗口销毁相关的任何关闭任务。在这种情况下，析构函数删除了构造函数中由 new 初始化的所有指针。

最后，在本模块中是 WindowCommand() 成员函数的实现。因为这只是一个简单的示例，所以这个函数并不大——实际上，它通常包含一个很长的 switch 语句，用于响应发送到此窗口的许多输入事件。在这里，只有一种可能的事件——当用户选择菜单的 File、Exit 命令时，由参数 id 等于常量 M_Exit 标识。

M_Exit 以及以 M_ 开头的其他常量在 v_defs.h 头文件中定义，该头文件包含在 TCmdWindow 实现模块的开头。你可以使用此类预定义的菜单命令常量（有几十个可用），也可以创建自己的常量。按惯例，为了区分这两种类型，请用小写 m_ 为你自己的菜单常量加上前缀。

WindowCommand() 的 switch 语句有两个 case。M_Exit 的 case 调用全局应用程序对象 theApp 的 Exit() 函数。这是结束 V 应用程序的正确方法。默认 case 调用祖先类的 WindowCommand() 函数来处理在应用程序级别未处理的任何事件。传递给 WindowCommand() 的三个参数的类型如下。因为为 V 应用程序编程主要涉及编写代码来响应事件（就像所有 X 应用程序一样），所以请仔细研究这些参数类型：

- **ItemVal id** 此值标识命令事件，例如菜单选择或按钮点击。它是一个唯一的整数值，通常在 switch 语句中用作 case 选择器。

- **ItemVal val** 此值包含某些但不是所有类型命令事件的附加信息。例如，val 可能是用户点击按钮的上下箭头时从微调按钮返回的值。

- **CmdType cType** 此值告诉你为此命令事件选择的对象类型。例如，如果 id 引用菜单命令，则 cType 等于 c_Menu。CmdType 是在 v_defs.h 中声明的枚举。它通常用于标识复选框（c_CheckBox）、标签（c_Label）以及对话框和工具栏中许多其他类型的视觉对象。

