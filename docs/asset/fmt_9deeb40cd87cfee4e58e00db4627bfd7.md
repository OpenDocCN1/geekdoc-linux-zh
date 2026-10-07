
```cpp
class WidgetImpl {
public:
    WidgetImpl() : m_parent(NULL), m_document(NULL) {};
    virtual ~WidgetImpl() {};
    virtual PRStatus Create() = 0;
    virtual PRStatus Show() = 0;
    virtual PRStatus Hide() = 0;
    virtual PRStatus Disable() = 0;
    virtual PRStatus Enable() = 0;
    virtual PRStatus SetGeometry(const int &x,
      const int &y, const int &width,
      const int &height, const char &mask) = 0;
    virtual PRStatus GetGeometry(int &x, int &y, int &width,
      int &height) = 0;
    virtual PRStatus SetParent(WidgetImpl *parent) = 0;
    virtual WidgetImpl* GetParent() = 0;
    virtual PRStatus SetType(ElementType type) = 0;
    virtual ElementType GetType() = 0;
    virtual PRStatus SetDocument(Document *document) = 0;
    virtual Document* GetDocument() = 0;
protected:
    WidgetImpl *m_parent;
    ElementType m_type;
    Document *m_document;
};
```

如你所示，`WidgetImpl` 与 `Control` 有许多共同点，同时也添加了自己的几个函数和变量。这让我们回到了一个问题：是否应该将 `Show()`、`Hide()`、`Enable()` 和 `GetGeometry()` 接口重构到一个公共基类 `WidgetCommon`？在 Trixul 的目前阶段，许多 Widget 需要实现，因此很难判断。重构接口的优势显而易见：这将强制平台特定类和平台中立类发生更改。然而，这样做可能会阻碍 `WidgetImpl` 独立变化的能力，并使其对工具包可能的要求产生抵抗。

到目前为止，我们看到的任何类（`WidgetImpl` 或 `ButtonImpl`）中都没有包含平台特定代码。这是没问题的，因为它们只是定义接口，对继承自它们的平台特定类施加规则。让我们转向这些平台特定类上。TriX 提供了 `ButtonImpl` 的三个具体实现——`CocoaButton`、`GtkButtonImpl` 和 `WindowsButtonImpl`。下面的列表定义了这些类。

## Cocoa

```cpp
#include "buttonimpl.h"
#import <Cocoa/Cocoa.h>
```

```cpp
#include "cocoawidgetimpl.h"
#include "commandhandler.h"
```

```cpp
class CocoaButtonImpl : public ButtonImpl,
public CocoaWidgetImpl, public CommandHandler

public:
```

## Trixul

```cpp
CocoaButtonImpl();
virtual ~CocoaButtonImpl();
virtual PRStatus Create();
virtual PRStatus Show();
virtual PRStatus Hide();
virtual PRStatus Enable();
virtual PRStatus Disable();
virtual PRStatus SetLabel(const string& label);
virtual PRStatus HandleCommand(const&);
virtual PRStatus GetGeometry(int &x, int &y, int &width, int &height);
virtual PRStatus SetGeometry(const int &x, const int &y, const int &width, const int &height, const char &mask);
```

private:

    NSButton *m_button;

};

## Gtk+

```cpp

#include "../buttonimpl.h"

#include <gtk/gtk.h>

```

```cpp

#include "gtkwidgetimpl.h"

```

```cpp

#include "commandhandler.h"

class GtkButtonImpl : public ButtonImpl,

public GtkWidgetImpl, public CommandHandler

{

public:

    GtkButtonImpl();

    virtual ~GtkButtonImpl();

    virtual PRStatus Create();

    virtual PRStatus Show();

    virtual PRStatus Hide();

    virtual PRStatus Enable();

    virtual PRStatus Disable();

    virtual PRStatus SetLabel(const string& label);

    virtual PRStatus HandleCommand();

    virtual PRStatus SetGeometry(const int &x, const int &y, const int &width, const int &height, const char &mask) {

        return SetGeometryImpl(x, y, width, height, mask);

    }

};

```

## 第 9 章 使用 C++ 开发跨平台 GUI 工具包

```cpp

virtual PRStatus GetGeometry(int &x, int &y, int &width, int &height) {

    return GetGeometryRequestImpl(x, y, width, height);

}

```

## Windows

```cpp

#include "buttonimpl.h"

#include <gcroot.h>

#using <mscorlib.dll>

#using <System.dll>

#using <System.Drawing.dll>

#using <System.Windows.Forms.dll>

```

```cpp

using namespace System;

using namespace System::ComponentModel;

using namespace System::Drawing;

using namespace System::Windows::Forms;

```

```cpp

#include "windowswidgetimpl.h"

#include "commandhandler.h"

#include "buttoncallbackhelper.h"

```

```cpp

class WindowsButtonImpl : public ButtonImpl,

public WindowsWidgetImpl, public CommandHandler

{

public:

    WindowsButtonImpl();

    virtual ~WindowsButtonImpl();

    virtual PRStatus Create();

    virtual PRStatus Show();

    virtual PRStatus Hide();

    virtual PRStatus Enable();

    virtual PRStatus Disable();

    virtual PRStatus SetLabel(const string& label);

    virtual PRStatus HandleCommand();

    virtual PRStatus SetGeometry(const int &x, const int &y, const int &width, const int &height, const char &mask);

```

## Trixel

# 459

```cpp

virtual PRStatus GetGeometry(int &x, int &y, int &width, int &height);

```

```cpp

private:

    groot<Button> m_button;

    groot<ButtonCallbackHelper> m_buttonHelper;

};

```

正如你可以看到的，这些类在某种程度上有所不同。这并不意外，因为这些类实现了特定平台的功能。第一个区别是，每个类都实现了一个特定平台的基类（`WindowsWidgetImpl`、`GtkWidgetImpl` 和 `CocoaWidgetImpl`）。这些类的意图是聚合仅在该平台上所有控件实现所需要的函数和成员变量。例如，`CocoaWidgetImpl` 维护了一个成员变量 `m_view`，Mac OS 上的控件类使用它来缓存一个 `NSObject` 对象，而其用法超出了本章的范围。它还定义了设置和获取该成员变量值的接口。同样，`GtkWidgetImpl` 为原生控件缓存了两个指向不同成员变量的指针，以及另一个用于在窗口中正确布局控件的指针。

另一个区别是，上述的每个类都引入了特定平台的头文件，并维护了持有原生控件接口指针的成员变量。（在 Gtk+ 中，所有控件都是 `Gtkwidget` 的实例，因此成员变量已提取到 `GtkwidgetImpl` 中。）

在我们继续之前，比较不同平台使用的代码是有趣的。`Create()` 函数执行了以下任务：

- 实例化一个平台控件（Gtk+ 使用 `GtkButton`，Cocoa 使用 `NSButton`，.NET Forms 使用 `Button`）。
- 注册一个回调函数，当用户点击按钮时调用。这允许我们通知监听者（稍后会详细介绍）。
- 将按钮设为其父视图的子级。

## 创建实现对象

以下是本书编写时 `WidgetImpl::Create()` 具体实现的源代码。由于在原生 GUI 工具包中执行这些操作的方式有所不同，上述每个任务（创建按钮、注册回调和设置按钮父子关系）的实现方式各不相同。

## 第 9 章 使用 C++ 开发跨平台 GUI 工具包

## Cocoa

在 Mac OS X 上，你首先会注意到所使用的语法非常奇特（至少对 C++ 来说是如此）。为了创建一个 `NSButton` 实例，你这些程序员需要执行以下操作：

```objc

m_button = [[NSButton alloc] initWithFrame:graphicsRect];

```

上述代码是用 Objective-C 编程语言编写的，这是除 Java 之外 Cocoa 接口支持的唯一编程语言。然而，我们可以直接从 C++ 调用 Objective-C 代码。以下代码显示了 Cocoa 平台的 `Create` 方法实现：

```cpp

PRStatus CocoaImpl::Create() {

    m_button = [[NSButton alloc] initWithFrame:graphicsRect];

    m_button setTarget:self;

    [m_button setAction:@selector(handleClick)];

    [view addSubview:m_button];

    return PR_OK;

}

```

（注：此处文本存在碎片化，上述逻辑是根据跨平台工具包的上下文重建的。）

## Trixel

# 487

```cpp

    NSView *parentView = (NSView *)self.view;

    if (parentView) {

        [parentView addSubview:m_button];

    }

    return PR_OK;

}

```

## Gtk+

Gtk+ 对 `ButtonImpl` 的实现在我看来是最简单的。在 Gtk+ 中，所有控件都是 `GtkFixed` 的实例，这允许我们根据其布局进行定位。（布局算法稍后讨论。）

```cpp

PRStatus GtkButtonImpl::Create() {

    m_widget = gtk_button_new();

    if (m_widget) {

        GtkFixed *container = GTK_FIXED(self.view);

        if (container) {

            gtk_fixed_put(container, GTK_WIDGET(m_widget), 0, 0);

        }

        g_signal_connect(m_widget, "clicked", G_CALLBACK(handle_callback), this);

    }

    return PR_OK;

}

```

## 第 9 章 使用 C++ 开发跨平台 GUI 工具包

## Windows

Trixul 使用 .NET Forms 原因有两个：

- Win32 和 MFC 已经是过去式了。
- .NET Forms 是微软设计的最清晰、最好的 API。该 API 比 Cocoa 或 Gtk+ 更直观，尽管有时确实有一些麻烦。

使用 .NET Forms 需要为 CLR 编译代码。CLR 是微软的通用执行环境。实际上，CLR 是一个抽象平台，类似于 Java 虚拟机。微软支持的语言（例如 Fortran、C、C#、COBOL 等）可以使用微软工具编译并在 CLR 上运行。此类代码被称为“托管”代码。Trixul 将托管代码隔离在一个 DLL 中，该 DLL 包含了类实现代码。该代码使用 Microsoft C++ 编译，与 Trixul 中的所有代码一样。然而，在 Windows 上编译和链接具体控件实现所需的编译器标志和链接选项对于构建托管代码是特定的，这在针对 .NET API 编码时是需要的。你可以下载 Trixul 源码并查看 `layout/windows` 下的 `Makefile.windows` 文件。

以下是 Windows 代码：

```cpp

PRStatus WindowsButtonImpl::Create() {

    m_button = __gc new Button();

    if (m_button) {

        if (m_formParent) {

            m_formParent->Controls->Add(m_button);

        } else if (m_svParent) {

            m_svParent->Controls->Add(m_button);

        }

    }

    return PR_OK;

}

```

## Trixul

```cpp

ButtonCallbackHelper *pHelper;

pHelper = m_buttonHelper =

    gc new ButtonCallbackHelper(this);

m_button->add_Click(

    new EventHandler(pHelper,

    &ButtonCallbackHelper::OnButtonClick));

    return PR_SUCCESS;

}

return PR_FAILURE;

```

## Widget Factories

现在我们已经看到了平台无关的 Button 类（以及它派生的类 Control 和 Widget），以及特定平台的 Button 派生类 `GtkButtonImpl`、`CocoaButtonImpl` 和 `WindowsButtonImpl`，接下来需要看 Trixul 如何实例化正确的平台特定类。通过某种方式，我们需要确保在 Gtk+ 上实例化的是 `GtkButtonImpl`，而不是 `WindowsButtonImpl`。为了实现这一点，我们使用了抽象工厂设计模式（Abstract Factory），该模式在《设计模式》（Addison-Wesley, 1995）中有所记载。

`WidgetFactory` 基类定义了用于创建平台特定组件实例的接口：

```cpp

class WidgetFactory {

public:

    virtual ~WidgetFactory() {};

    virtual AppImpl* MakeApp() = 0;

    virtual ButtonImpl* MakeButton() = 0;

    virtual GridListImpl* MakeGridList() = 0;

    virtual StaticTextImpl* MakeStaticText() = 0;

    virtual TextImpl* MakeText() = 0;
```
