
```c
{ "/File/sep1", 0, 0, 0, "<Separator>" },

{ "/File/Quit", "<control>Q", gtk_main_quit, 0, 0 }

};

};

GtkAccelGroup *accel_group;

int n_items = sizeof(menu_items) / sizeof(menu_items[0]);

GtkItemFactory *factory = item_factory;

accel_group = gtk_accel_group_new();

item_factory = gtk_item_factory_new(

    GTK_TYPE_MENU_BAR, "main", accel_group);

gtk_item_factory_create_items(item_factory,

    n_items, menu_items, (void *)"foo");

gtk_accel_group_attach(accel_group,

    GTK_OBJECT(m_window));

GtkWidget *menubar;

menubar = gtk_item_factory_get_widget(

    item_factory, "<main>");

gtk_box_pack_start(GTK_BOX(m_main_vbox), menubar,

    FALSE, FALSE, 0);

gtk_widget_show(menubar);

return 0;

}
```

## 使用发布/订阅在视图和模型之间进行通信

现在已经理解支持 GUI 的基本结构，还有一个最后一个细节需要讨论。该细节是 `ProcessList` 类如何将进程列表通信给 GUI 类。简而言之，我们希望模型（`ProcessList`）告诉视图（`GUI`）它发现的每一个进程。

## 项目 22：将用户界面与模型分离

当模型告知某个进程时，视图会将该进程（包括其名称和 PID）添加到滚动列表中进行显示。

实现模型与视图之间的通信可以使用观察者（或发布/订阅）设计模式。观察者设计模式基于“不要来找我们，我们会来找你”的范式。在这种范式中，观察者（在本例中为实现视图的 `GUI` 对象）向主题（实现模型的 `ProcessList` 对象）注册自己。观察者与主题之间的契约是由主题定义的接口——为了参与其中，观察者必须实例化一个继承自该接口的对象，并在注册自己时将该对象的指针传递给主题。主题将此指针置于列表中；当到了它需要与当前在列表中的观察者进行通信时，它会遍历列表，并调用其上的每个对象。在我们的应用程序中，主题接口只定义了一个函数：`OnNewProcess()`。当模型查询操作系统获取当前进程列表时，每读取一个进程，该函数就会为该进程调用一次。以下代码定义了观察者必须实现的接口：

```cpp
#if __PROCESSLISTENER_H__

#define __PROCESSLISTENER_H__

class ProcessListener
{
public:
    virtual ~ProcessListener() {};
    virtual void OnNewProcess(const char *name,
        const int pid) = 0;
};

#endif
```

注意 `OnNewProcess()` 是纯虚的，要求继承自 `ProcessListener` 的类来实现它。通过使用此接口，列表中的每个进程都会向视图传递两个参数：进程名称和其 PID。我们可能会选择扩展此类，以包含一个在进程从列表中移除时被调用的函数，但为了保持简单，我们现在只关注这里的这一个函数。

为了允许观察者在主题处注册（及注销）自己，主题需要继承或实现为此目的的接口。

# 第7章 用户界面

在以下代码中，执行这些操作的分别是 `RegisterListener()` 和 `UnregisterListener()`：

```cpp
#if defined(__PROCESSPUBLISHER_H__)

#define __PROCESSPUBLISHER_H__
```
```cpp
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
    std::list<ProcessListener *> m_listeners;
};

#endif
```

这两个函数都接受一个继承自之前定义的 `ProcessListener` 的指针作为参数。以下是 `ProcessPublisher` 的实现。`RegisterListener()` 和 `UnregisterListener()` 函数是非常简单的，分别用于 STL 列表中添加和移除观察者。`SendNotification()` 由模型调用，用于通知所有观察者检测到了一个进程。它的参数是一个简单的类，用于管理单个进程的 PID 和名称：

```cpp
#include "processpublisher.h"
#include "processlistener.h"
```
```cpp
void ProcessPublisher::RegisterListener(ProcessListener *listener) {
    if (listener) {
        m_listeners.push_back(listener);
    }
}
```

## 项目 22：将用户界面与模型分离

```cpp
void ProcessPublisher::UnregisterListener(ProcessListener *listener) {
    if (listener) {
        m_listeners.remove(listener);
    }
}

void ProcessPublisher::SendNotification(Process &proc) {
    std::list<ProcessListener>::iterator iter;
    for (iter = m_listeners.begin(); iter != m_listeners.end(); ++iter) {
        (*iter)->OnNewProcess(proc.GetName(), proc.GetPID());
    }
}
```
