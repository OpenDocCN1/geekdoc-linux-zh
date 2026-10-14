

## LISTING 30.2 VWELCOME.CPP

```
#include "cmdwin.h"    // Include command window header
#include "app.h"       // Include application module header

// Construct the application object
static TWelcomeApp WelcomeApp(APPNAME);

// Main function
int AppMain(int argc, char* argv[])
{
    theApp->NewAppWin(0, TITLE, 325, 50);
    return 0;
}
```

应用程序对象是一个派生自 vApp 的类的全局静态变量。在本例中，我将应用程序类命名为 TWelcomeApp，全局对象命名为 WelcomeApp。APPNAME 是一个表示应用程序名称的字符串常量。TITLE 是窗口标题字符串。

函数 AppMain() 类似于常规程序中的 main() 函数。它具有 argc 和 argv 参数用于使用任何命令行选项，尽管示例程序忽略了这些变量。在 AppMain() 内部，第一条语句调用由 theApp 寻址的对象的新建应用窗口 NewAppWin() 成员函数。这是一个全局 V 指针，它寻址主应用程序对象——在本例中为 WelcomeApp。传递给 NewAppWin() 的四个参数如下：

- 0 这是一个空窗口* 指针值，但它可以寻址一个已存在的窗口（可能是派生类 vCmdWindow 的），如果出于某种原因你想在初始化应用程序之前创建该对象。
- TITLE 这是一个标准的 C 风格、以空字符结尾的字符串，表示窗口标题。因为 V 基于小部件（至少在 UNIX 和 Linux 中），你可以确信窗口标题会出现在其框架顶部，这与纯 Xlib 编程不同，后者并不能保证类似的行为。
- 325 这是窗口框架建议的宽度，以像素为单位。
- 50 这是窗口框架建议的高度，以像素为单位。

使用 theApp 指针而不是直接使用对象有两个主要原因。首先，许多其他模块需要引用这个关键对象，其次，在较大的程序中，你可能在单独的模块中定义应用程序对象，也许是为了将其隐藏起来。无论如何，你始终可以使用 theApp 来寻址主应用程序对象。

### Note

> 由于 X 服务器、客户端应用程序和窗口管理器的工作方式，你不能指望 AppMain() 会返回。但是，你可以确信主应用程序对象的类析构函数会在控制权返回到启动你的客户端程序的进程之前被调用。这意味着你的主应用程序对象总是有最后一次机会在程序结束前执行关键任务——例如保存文件。

## THE APPLICATION CLASS

主应用程序对象是从本节模块中声明并实现的类构造的。Listing 30.3, app.h，显示了 TWelcomeApp 类的声明。

## LISTING 30.3 WELCOME/APP.H

```
#include <v/vapp.h>  // Need vApp class

#define APPNAME "Welcome"
#define TITLE "Welcome to V Programming for X"

// Application class
//
class TWelcomeApp : public vApp {
public:
TWelcomeApp(char* name) : vApp(name) {}
virtual ~TWelcomeApp() {}
virtual vWindow* NewAppWin(vWindow* win, char* name,
int h, int w, vAppWinInfo* winInfo);
};
```

包含 vapp.h 头文件以使 vApp 基类可用。也定义了在 vwelcome.cpp 模块中用于初始化程序并为窗口提供标题的应用程序和标题字符串。

按 TWelcomeApp 所示派生你的应用程序类。至少，派生类需要一个构造函数、一个虚析构函数，以及一个虚成员函数 NewAppWin()。在本例中，构造函数和析构函数没有新的职责要执行，并且以内联方式实现。构造函数调用其祖先构造函数 vApp()。虚基类析构函数会自动调用。如前一节所述，主应用程序模块调用 NewAppWin() 来创建程序的主窗口。

> Note
> 严格来说，你可以从派生应用程序类析构函数和其他函数中删除 virtual 这个词。这是因为，即使基类声明成员函数为 virtual，派生类也只有在另一个类将从它派生时才需要这样做。我提到这一细节是因为，在浏览 V 源代码示例时，你可能会遇到成员函数以两种方式声明的情况。

Listing 30.4, app.cpp，显示了 TWelcomeApp 类的实现。因为该类的构造函数和析构函数以内联方式实现，app.cpp 文件只包含一个函数的编程，即 NewAppWin()。

