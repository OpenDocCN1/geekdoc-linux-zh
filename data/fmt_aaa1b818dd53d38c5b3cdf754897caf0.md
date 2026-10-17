
`GUI::MainLoop()`

```cpp
{
    if (m_guiImpl)
        return m_guiImpl->MainLoop();
    return -1;
}
```

```cpp
int
GUI::Shutdown()
{
    if (m_guiImpl)
        return m_guiImpl->Shutdown();
    return -1;
}
```

注意 `CreateUI()` 的结构，它与其他函数不同之处在于调用了两个平台特定的函数：一个创建滚动列表的主窗口，另一个创建应用程序的菜单栏和菜单。这种选择是随意的——我本可以在实现类中进一步划分，从而简化这一层的工作。然而，在这里这样做展示了你在代码实现方面的灵活性。为应用程序提供所需的 API 并不重要。

在我们讨论 `GUIImpl` 实现类之前，值得看看 `GUI` 类是如何在应用程序中。以下列表提供了细节：

```cpp
#include <stdio.h>
#include "processes.h"
#include "gui.h"
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

在前面的代码中，调用 `Scan()` 获取进程列表并将其传递给 `GUI`。

## 项目 22：分离用户界面与模型

首先，让我们看看每个平台的实现类。`GUI` 类是抽象的，并定义了接口。

```cpp
#if defined(__GUI_IMPL__)
#define __GUI_IMPL_H__
class GUIImpl {
public:
    GUIImpl() {};
    virtual ~GUIImpl() {};
    virtual int Init(int argc, char *argv[]) = 0;
    virtual int CreateMenus() = 0;
    virtual int CreateProcessListWindow() = 0;
    virtual int Shutdown() = 0;
    virtual int AddProcess(const char *name, const int pid) = 0;
    virtual int ClearList() = 0;
};
#endif
```

这里没有惊喜；实现类是抽象的，并定义了接口。以下列表分别说明了 Cocoa、.NET Forms 和 Gtk+。每个类都实现了相同的接口，但具有特定平台的私有实现。

### Cocoa

```cpp
class CocoaGUIImpl : public GUIImpl {
public:
    CocoaGUIImpl();
    virtual ~CocoaGUIImpl();
    virtual int Init(int argc, char *argv[]);
    virtual int MainLoop();
    virtual int CreateMenus();
    virtual int CreateProcessListWindow();
    virtual int Shutdown();
    virtual int AddProcess(const char *name, const int pid);
    virtual int ClearList();
private:
    int CreateAppleMenu();
    int CreateCreateWindow();
    int CreateScrolledlist(NSRect graphicsRect);
    NSoreleasePool *m_pool;
    NSMenu *m_menubar;
    NSView *m_view;
    NSWindow *m_window;
    NSTableView *m_gridlist;
    NSScrollView *m_scrolledwindow;
    GridlistDataSource *m_dataSource;
    NSMenuItem *m_preferencesMenuItem;
    NSMenuItem *m_quitMenuItem;
    NSTableColumn *m_pidColumn;
    NSTableColumn *m_nameColumn;
};
```

### .NET Forms/Windows

```cpp
#if defined(__WINDOWSGUIMPL_H__)
#define __WINDOWSGUIMPL_H__
#include "../guimpl.h"
#include <gcroot.h>
#using <mscorlib.dll>
#using <System.dll>
#using <System.Drawing.dll>
#using <System.Windows.Forms.dll>
namespace System {
using System::Data;
using System::ComponentModel;
using System::Drawing;
using System::Windows::Forms;
class WindowsGUIImpl : public GUIImpl {
public:
    WindowsGUIImpl();
    virtual ~WindowsGUIImpl();
    virtual int Init(int argc, char* argv[]);
    virtual int MainLoop();
    virtual int CreateMenus();
    virtual int CreateProcessListWindow();
    virtual int Shutdown();
    virtual int AddProcess(const char* name, const int pid);
    virtual int ClearList();
private:
    int HandleCommand();
    gcroot<DataGrid> m_gridlist;
    gcroot<Form> m_form;
    gcroot<Panel> m_panel;
    gcroot<DataTable> m_processTable;
};
}
#endif
```

### Gtk+

```cpp
class GtkGUIImpl : public GUIImpl {
public:
    GtkGUIImpl();
    virtual ~GtkGUIImpl();
    virtual int Init(int argc, char *argv[]);
    virtual int MainLoop();
    virtual int CreateMenus();
    virtual int CreateProcessListWindow();
    virtual int Shutdown();
    virtual int AddProcess(const char *name, const int pid);
    virtual int ClearList();
private:
    GtkWidget *m_window;
    GtkBox *m_vbox;
    GtkLabel *m_label;
    GtkTreeView *m_treeview;
    GtkTreeModel *m_treelist;
};
```

为了说明此层次代码的特定平台特性，以下列表显示了 Gtk+ 的 `CreateMenus()` 实现。Cocoa 的实现未显示，使用 Objective-C++ 编写，要复杂得多。.NET Forms 的实现未显示，使用 Managed C++ 编写：

### 318

## 第7章 用户界面

```cpp
int LinuxGUIImpl::CreateMenus()
{
    static GtkFactoryEntry menu_items[] = {
        { "/File", 0, 0, 0, "<Branch>" },
```
