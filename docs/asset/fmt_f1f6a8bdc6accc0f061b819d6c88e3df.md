
```cpp
GUI::Init(int argc, char *argv[],

    ProcessList +processes)

{

    // 现在暂忽略 processes 参数

    if (m_guiImpl)

        return m_guiImpl->Init(argc, argv);

    return -1;

}

int

GUI::CreateUI()

{

    int ret = -1;

    if (m_guiImpl) {

        if (!ret = 

            m_guiImpl->CreateProcessListWindow())

            return m_guiImpl->CreateMenus();

        }

    }

    return -1;

}

int

GUI::MainLoop()

{

    if (m_guiImpl)

        return m_guiImpl->MainLoop();

    return -1;

}

int

GUI::Shutdown()

{

    if (m_guiImpl)

        return m_guiImpl->Shutdown();

    return -1;

}
```

注意 `Create()` 的结构，它与其他函数不同，之处在于它调用了两个特定平台的函数，一个用于创建显示滚动列表的主窗口，另一个用于创建应用程序的菜单栏和菜单。

## 事项 22：将用户界面与模型分离

这种做法的选择带有某种随机性——我本可以在实现类更靠后的位置进行分割，从而简化这一层级的工作。然而，在这里这样做说明了在这一层面的代码实现上你具有一定的灵活性。重要的是应用程序的 API 是抽象的。为了提供所需的功能，在实现类中需要调用什么函数并不重要。

在我们继续讨论实现类 `GUIImpl` 之前，值得看一眼 `GUI` 类在应用程序中是如何被使用的。下面的代码列表（相关代码已**加粗**显示）提供了详细信息：

```cpp

#include <stdio.h>

#include "processes.h"

#include "gui.h"

int

main(int argc, char *argv[])

{

    ProcessList processList;

    GUI *gui;

gui = GUI::GetInstance();

    if (gui) {

        gui->Init(argc, argv, &processList);

        gui->CreateUI();

    }

    processList.Scan();

    gui->MainLoop();

}

```

在前面的代码中，调用 `Scan()` 是为了获取进程列表，并在进入 GUI 主循环之前将其传递给 GUI。通常，操作是作为用户交互的结果执行的，例如点击按钮或选择菜单项。然而，在这个简单的示例中，将调用放置在 `main()` 中就足够了，该调用是在 GUI 创建之后、进入主循环之前完成的。你稍后会看到 `Scan()` 函数内部发生了什么，从而将 `ProcessList` 类和 `GUI` 类结合在一起。

## GUI 实现类

但首先，让我们看看每个平台的实现类。首先是 `GUIImpl` 类，它定义了抽象类 `GUI` 调用的接口（如前文所示），并且平台特定的实现类都都继承自它：

```cpp

#if defined(__GUI_IMPL_H__)

#define __GUI_IMPL_H__

class GUIImpl {

public:

    GUIImpl() {};

    virtual ~GUIImpl() {};

    virtual int Init(int argc, char argv[]) = 0;

    virtual int CreateMenus() = 0;

    virtual int CreateProcessListWindow() = 0;

    virtual int Shutdown() = 0;

    virtual int AddProcess(const char *name, const int pid) = 0;

    virtual int ClearList() = 0;

};

#endif

```

这里应该没有意外；实现类是抽象的，它定义了 `GUI` 类通过工厂提供的 `GUIImpl` 指针调用的每个接口。有三个类，每个对应一个支持的平台，实例化 `GUIImpl` 的派生类。下面的列表分别展示了 Cocoa、.NET Forms 和 Gtk+ 的这些类。注意的是，每个类都实现了相同的公共接口，但具有非常不同的私有实现，由该类所支持的平台 GUI 工具包特定的函数和成员变量组成。只要公共接口一致，该类就可以且通常必须实现针对平台 GUI 工具包所需的私有代码。正如你在后续列表中所示，Cocoa 的私有实现最复杂，而 Gtk+ 是三者中最简单的。

## 事项 22：将用户界面与模型分离

### Cocoa/MacOS X

```objc

#if defined(__COCOAGUIIMPL_H__)

#define __COCOAGUIIMPL_H__

```

```objc

#include "../guiimpl.h"

#import <Cocoa/h.h>

#import <gridlistdatasource.h>

```

```objc

class CocoaGUIImpl : public GUIImpl {

public:

    CocoaGUIImpl();

    virtual ~CocoaGUIImpl();

    virtual int Init(int argc, char *argv[]);

    virtual int MainLoop();

    virtual int CreateMenus();

    virtual int CreateProcessListView();

    virtual int Shutdown();

    virtual int AddProcess(const char *name, const int pid);

    virtual int ClearList();

private:

    int CreateMenusInternal();

    int AddToMenuBar(NSMenu *menu);

    int SetPreferencesMenuItem(NSMenuItem *item);

    void SetQuitMenuItem(NSMenuItem *item);

    int CreateWindow(NSR rect);

    int CreateScrolledList(NSR rect);

    AutoreleasePool *pool;

    NSMenu *menubar;

    NSView *view;

    NSWindow *window;

    NSTableView *gridlist;

    GridListDataSource *dataSource;

    NSMenuItem *preferencesMenuItem;

    NSMenuItem *quitMenuItem;

    NSTableColumn *pidColumn;

    NSTableColumn *nameColumn;

};

#endif

```

### .NET Forms/Windows

```cpp

#if defined(__WINDOWSIMPL_H__)

#define __WINDOWSIMPL_H__

#include "../guiimpl.h"

#include <iostream>

#using mscorlib.dll

#using System.dll

#using System.Drawing.dll

#using System.Windows.Forms.dll

namespace System {

    using Data;

    using Component;

    using Drawing;

    using Forms;

}

class WindowsGUIImpl : public GUIImpl {

public:

    WindowsGUIImpl();

    virtual ~WindowsGUIImpl();

    virtual int Init(int argc, char *argv[]);

    virtual int MainLoop();

    virtual int CreateMenus();

    virtual int CreateProcessListWindow();

    virtual int Shutdown();

    virtual int AddProcess(const char *name, const int pid);

    virtual int ClearList();

    int HandleCommand();

private:

    gcroot<DataGrid> gridlist;

    gcroot<Form> form;

    gcroot<Panel> panel;

    gcroot<DataTable> processTable;

};

#endif

```

### Gtk+/Linux

```cpp

#if defined(__LINUXGUIIMPL_H__)

#define __LINUXGUIIMPL_H__

#include "../guiimpl.h"

#include <gtk/gtk.h>

class LinuxGUIImpl : public GUIImpl {

public:

    LinuxGUIImpl();

    virtual ~LinuxGUIImpl();

    virtual int Init(int argc, char *argv[]);

    virtual int MainLoop();

    virtual int CreateMenus();

    virtual int CreateProcessListWindow();

    virtual int Shutdown();

    virtual int AddProcess(const char *name, const int pid);

    virtual int ClearList();

private:

    GtkWidget *window;

    GtkWidget *main_vbox;

    GtkWidget *clist;

};

#endif

```

# 318

## 第7章 用户界面

```cpp

int LinuxGUIImpl::CreateMenus()

{

    static GtkFactoryEntry menu_items[] = {

        "/File", 0, 0, 0, "<Branch>",

        "/File/sep1", 0, 0, 0, "<Separator>",

        "/File/Quit", "<control>",

        gtk_main_menu_quit, 0, 0

    };

    GtkAccelGroup *accel_group = NULL;

    int nmenu_items = sizeof(menu_items) /

        sizeof(menu_items[0]);

    GtkItemFactory *item_factory = NULL;

    accel_group = gtk_accel_group_new();

    item_factory = gtk_item_factory_new(

        GTK_TYPE_MENU_BAR, "<main>", accel_group);

    gtk_item_factory_create_items(item_factory,

        nmenu_items, menu_items, (void*)"foo");

    gtk_accel_group_attach(accel_group,

        GTK_OBJECT(m_window));

    GtkWidget *menubar = NULL;

    menubar = gtk_item_factory_get_widget(

        item_factory, "<main>");

    gtk_box_pack_start(GTK_BOX(m_main_vbox), menubar,

        FALSE, FALSE, 0);

    gtk_widget_show(menubar);

    return 0;

}

```

## 使用发布/订阅模式在视图和模型之间进行通信

现在我们已经理解了支持 GUI 的基本结构，还有一个最后的细节需要讨论。该细节就是 `ProcessList` 类如何将进程列表传递给 GUI 类。简单而言之，我们希望模型（`ProcessList`）告诉视图（GUI）它发现的每一个进程。

### 事项 22：将用户界面与模型分离

当被模型通知某个进程时，视图会将该进程（包括其名称和 PID）添加到滚动列表中进行显示。

模型与视图之间的通信可以使用观察者（或发布/订阅）设计模式来实现。观察者设计模式基于“不要来叫我们，我们会来叫你”的范式。在这个范式中，观察者（在本例中是实现视图的 GUI 对象）向主体（实现模型的 `ProcessList` 对象）注册自己。观察者与主体之间的契约是由主体定义的接口——为了参与，观察者必须实例化一个继承该接口的对象，并在注册自己时将该对象的指针传递给主体。主体将此指针放入一个列表；当需要它与当前在列表中的观察者进行通信时，它会遍历列表并调用其上的每个对象。在我们的应用程序中，主体接口定义了一个函数 `OnNewProcess()`。每当模型查询操作系统获取当前进程列表并读取到进程时，就会为每个被读取的进程调用一次该函数。以下代码定义了观察者对象必须实现的接口：

```cpp

#if __PROCESSLISTENER_H__

#define __PROCESSLISTENER_H__

class ProcessListener{

public:

    virtual ~ProcessListener() {};

    virtual void OnNewProcess(const char *name, const int pid) = 0;

};

#endif

```

注意 `OnNewProcess()` 是纯虚函数，要求自 `ProcessListener` 的类实现它。对于列表中的每个进程，模型通过此接口向视图传递两个参数：进程的名称和它的 PID。我们可能会选择这个类以包含一个在进程从列表中移除时调用的函数，但为了保持简单，我们在这里只关注这一个函数。

为了允许观察者向主体注册（并取消注册），主体需要继承或实现为此目的的接口。

在下面的代码中，执行这些操作的函数分别是 `RegisterListener()` 和 `UnregisterListener()`：

```cpp

#if defined(__PROCESSPUBLISHER_H__)

#define __PROCESSPUBLISHER_H__

class ProcessListener;

#include "process.h"

#include <list>

class ProcessPublisher {

public:

    virtual ~ProcessPublisher() {};

    void RegisterListener(ProcessListener *listener);

    void UnregisterListener(ProcessListener *listener);

    void SendNotification(Process &proc);

private:

    std::list<ProcessListener*> m_listeners;

};

#endif

```

这两个函数都接受一个指向继承自之前定义的 `ProcessListener` 对象的指针。以下是 `ProcessPublisher` 的实现。`RegisterListener()` 和 `UnregisterListener()` 函数非常简单，分别用于从 STL 列表中添加和删除观察者。`SendNotification()` 被调用以通知所有观察者检测到了一个进程。它的参数是一个简单的类，用于管理单个进程的 PID 和名称：

```cpp

#include "processpublisher.h"

#include "processlistener.h"

void ProcessPublisher::RegisterListener(ProcessListener *listener) {

    if (listener) {

        m_listeners.push_back(listener);

    }

}

void ProcessPublisher::UnregisterListener(ProcessListener *listener)

{

    if (listener)

        m_listeners.remove(listener);

}

void ProcessPublisher::SendNotification(Process &proc)
{
