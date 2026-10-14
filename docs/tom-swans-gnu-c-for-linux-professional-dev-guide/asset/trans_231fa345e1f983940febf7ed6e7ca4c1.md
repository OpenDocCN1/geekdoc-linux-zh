

## 主要应用程序

V 程序的引擎是其主应用程序对象。该对象使用类构造函数初始化程序并启动程序的运行。应用程序类的析构函数执行任何清理工作，例如将客户端与 X 服务器断开连接。每个 V 应用程序必须有且只有一个主应用程序对象。

要创建应用程序对象，请从 VApp 派生一个应用程序类并填充几个成员函数。清单 29.1 显示了生成的 main 应用程序类声明（以 myapp.cpp 作为源代码重新格式化代码并删除了一些多余的注释以节省空间）。

```cpp
#include <v/vapp.h>
#include <v/vawinfo.h>

class myApp : public vApp {
    friend int AppMain(int, char**); // allow AppMain access
public:
    myApp(char* name, int sdi = 0, int h = 0, int w = 0);
    virtual ~myApp();
    // Routines derived from vApp that are normally overridden
    virtual vWindow* NewAppWin(vWindow* win, char* name,
        int w, int h, vAppWinInfo* winInfo);
    virtual void Exit(void);
    virtual int CloseAppWin(vWindow*);
    virtual void AppCommand(vWindow* win,
        int itemVal, int subItemVal, CmdType type);
    virtual void Key(vWindow* v, vKey, unsigned int);
protected:
private:
    myCmdWindow* _myCmdWin; // Pointer to first window instance
};
```

vApp 类在 V3 的 vapp.h 头文件中声明。在程序的主应用程序文件中包含该头文件以及 vawinfo.h。第二个头文件声明了一个类 vAppWinInfo，该类似乎没有多大实际价值，但为了与早期 V 版本向后兼容而包含在内（有关该类的更多信息，请参阅在线文档）。

如清单所示，从 vApp 派生你的应用程序类。你可以随意命名你的类，但为了清晰起见，它应以 App 结尾。派生类中的第一项是 AppMain() 的友元函数声明，使该函数可以访问 myApp 的私有和受保护声明。AppMain() 等同于 C 或 C++ 程序的 main() 函数。V 应用程序完全面向对象，并且使用对象来构造和销毁应用程序。V 应用程序没有 main() 函数。

myApp 类中的其他声明覆盖了 vApp 基类的各种成员函数。根据你的需要，你可以添加或删除生成的函数——但这些在大多数应用程序中通常是必需的。你可以在类的 protected 部分添加其他声明，默认情况下该部分为空。单个私有数据成员定义了指向下一节中讨论的 myCmdWindow 类对象的指针。通过此指针，主应用程序对象访问程序的顶级命令窗口。

> **注意**
>
> 按照惯例，V 会用下划线为私有数据成员（如 `_myCmdWin`）加前缀。当你遇到类似拼写的变量时，你就知道它是类的私有成员，因此只能从该类的成员函数访问。

清单 29.2，myapp.cpp，显示了类声明中原型函数的一些实现。我删除了一些不执行新操作的函数，并且再次重新格式化了文本以节省空间。

### LISTING 29.2 MYAPP.CPP (PARTIAL)

```cpp
#include "myapp.h"  // Header file

myApp::myApp(char* name, int sdi, int h, int w) :
 vApp(name, sdi, h, w)
{
    // Constructor
    _myCmdWin = 0;
}

myApp::~myApp()
{
    // Destructor
}

vWindow* myApp::NewAppWin(vWindow* win, char* name,
 int w, int h, vAppWinInfo* winInfo)
{
    vAppWinInfo* awinfo = winInfo;
    char *appname = name;

    if (!*name) {
        appname = "Hello to V Programming";  // Default name
    }

    UserDebug( Build, "myApp::NewAppWin(%s)\n", appname);

    // Create the first window using provided CmdWindow
    _myCmdWin = (myCmdWindow*) win;
    if (!_myCmdWin) {
        _myCmdWin = new myCmdWindow(appname, w, h);
    }

    if (!awinfo)
        awinfo = new vAppWinInfo(appname);
    return vApp::NewAppWin(_myCmdWin, appname, w, h, awinfo);
}

void myApp::Exit(void)
{
```
