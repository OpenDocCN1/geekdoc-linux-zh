

## LISTING 30.4   WELCOME/APP.CPP

```
#include "app.h"          // Need TWelcomeApp
#include "cmdwin.h"       // Need TCmdWindow
#include <vavinfo.h>       // Need unused vAppWinInfo class

// Construct a new application window
vWindow* TWelcomeApp::NewAppWin(vWindow* win, char* name,
    int w, int h, vAppWinInfo* winInfo)
{
    vWindow* localWin = win;          // Local parameter copies
    vAppWinInfo* localInfo = winInfo;
    char* localName = name;

    if (!localName)
        localName = TITLE;
    if (!localWin)
        localWin = new TCmdWindow(localName, w, h);
    if (!localInfo)
        localInfo = new vAppWinInfo(localName);
    return vAppWindow::NewAppWin(localWin, localName, w, h, localInfo);
}
```

该模块包含三个头文件。第一个是其自身的头文件，声明了 TWelcomeApp 类。接下来是头文件 cmdwin.h，声明了程序的 TCmdWindow 类，用于表示主窗口——下一节将详细介绍。第三个头文件 vavinfo.h 声明了类 vAppWinInfo，该类对 NewAppWin() 函数是必需的，但本质上未被使用。

NewAppWin() 成员函数创建了两个对象。第一个是 TCmdWindow 类的对象。第二个是 vAppWinInfo 类型的对象。这些类构造函数的参数提供了窗口的建议宽度和高度以及应用程序名称字符串。利用 resulting 对象指针，最后一步是调用祖先类的 NewAppWin() 函数。无论你的程序多么复杂，这些步骤很可能就是你的 NewAppWin() 函数需要执行的所有操作。

刚接触面向对象编程的读者可能会觉得这一步缺少了什么。但请记住要以对象为思考方式。信任 vApp 类中的祖先 NewAppWin() 函数来完成创建程序窗口所需的任何操作。在应用程序级别，你的代码只需要做程序所需的额外工作。作为这种设计方法的良好示例，我们的 vWelcome 应用程序对象只需要创建程序的窗口对象——该窗口具体做什么是由窗口类负责的，如下所述。

## THE COMMAND WINDOW CLASS

vWelcome 应用程序中的最后一个模块声明并实现了程序的命令窗口类。V 中的命令窗口是可以接收输入并显示图形输出的窗口。在 X 中，窗口就是行动发生的地方，你可以认为 V 命令窗口是程序的行动模块。Listing 30.5, cmdwin.h，展示了 vWelcome 的 TCmdWindow 类的声明。

## LISTING 30.5 VWELCOME/CMDWIN.H

```
#include <v/canvas.h>  // Need vCanvasPane class
#include <v/menu.h>  // Need vMenuPane class
#include <v/cmdwin.h>  // Need vCmdWindow class

// Command window class
class TCmdWindow : public vCmdWindow {
private:
  vCanvasPane* myCanvas;  // Pointer to window's canvas
  vMenuPane* myMenu;  // Pointer to window's menu
public:
  TCmdWindow(char* name, int width, int height);
  virtual ~TCmdWindow();
  virtual void WindowCommand(ItemVal id, ItemVal val,
    CmdType cType);
};
```

命令窗口类模块通常至少需要包含这里的三个头文件。第一个 vcanvas.h 声明了 vCanvasPane，用于表示窗口的内部绘图表面——简称为“画布”。vmenu.h 头文件声明了 vMenuPane 类，用于表示窗口的菜单栏。这不是严格必需的，但大多数 X 应用程序都应具有下拉菜单栏。第三个头文件包含 vcmdwin.h，其中声明了我们的类派生的 vCmdWindow 类。

该类 TCmdWindow 以两个私有数据成员声明开始。其中第一个 myCanvas 是指向 vCanvasPane 对象的指针。所有对该窗口的输出都通过此指针进行。第二个私有成员是指向 vMenuPane 对象的指针 myMenu。正如你可能猜到的，这个指针指向表示窗口下拉菜单的对象。

由于指针对类是私有的，TCmdWindow 对象拥有所指向的对象。这样，V 命令窗口拥有其画布和菜单栏，以及你稍后会学到的其他元素，如工具栏和状态栏。这是一种合理且易于使用的设计。由于命令窗口拥有其菜单栏和其他元素，因此控制这些项目的地点在命令窗口模块中。

### Tip

> 请记住，当一个对象拥有另一个对象时，这并不意味着在类级别存在任何关系。在学习任何新的类库时，通过继承相关联的类与通过对象所有权相关联的类的区别是最重要的区别之一。（V 的在线类层次结构图清楚地显示了这些关系。）

除了其私有数据成员之外，TCmdWindow 类还声明了三个函数：构造函数、虚析构函数和虚函数 WindowCommand()。顾名思义，该函数负责响应发送到此窗口的命令——例如，用户选择下拉菜单命令时作出响应。Listing 30.6, cmdwin.cpp，实现了 vWelcome 的 TCmdWindow 类。

