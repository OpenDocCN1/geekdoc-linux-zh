
由于`C++`编译器比`C`编译器提供更好的编译时错误检查，如果你不使用`C++`的面向对象特性（例如，不使用类定义），我建议使用`C++`而不是`C`。

### 使用`C++`类库处理`Athena`组件

在本节中我们将学习一个非常简单的`C++`库，它封装了以下`Athena`组件：

| 组件 | 说明 |
| --- | --- |
| `PanedWindow` | 封装在`C++`类中（该类也会生成一个顶层组件）。 |
| `Label` | 封装在`C++`类`Label`中。 |
| `Command Button` | 封装在`C++`类`Button`中。 |
| `AsciiText` | 封装在`C++`类`Text`中。 |

作为这个练习的动力，我将首先展示一个完全不包含（明显的）`X Windows`代码的测试程序。示例程序`test_it.cpp`位于`src/X/c++`目录，列如下。

`iostream.h`定义了标准的`C++ I/O`。包含文件`PanedWindow.h`、`Label.h`、`Button.h`和`Text.h`定义了我们封装相应`Athena`组件的`C++`类：

```cpp
#include <iostream>
#include "PanedWindow.h"
#include "Label.h"
#include "Button.h"
#include "Text.h"
```

我们将创建这些`C++`对象中的每一个。按钮将有一个回调函数，用于打印文本对象的内容。我们将`Text`对象设为全局，以便`button_cb`回调函数可以访问它：

```cpp
Text *text;
```

`button_cb`回调函数使用`text`打印：

```cpp
void button_cb() {
    std::cout << text->getText() << std::endl;
}
```

`main`函数如下：

```cpp
int main(int argc, char *argv[]) {
    Widget top_level, url;
    top_level = XtInitialize(argv[], "url", NULL, &argc, argv);
    Arg args[3];
    XtSetArg(args[0], XtNwidth, 520);
    XtSetArg(args[1], XtNheight, 580);
    XtSetArg(args[2], XtNURLResource, "www.knowledgebooks.com");
    url = XtCreateManagedWidget("url", URLWidgetClass, top_level, args, 3);
    XtRealizeWidget(top_level);
    XtMainLoop();
    return 0;
}
```

# 用户界面编程

## 第四部分

```cpp
void addComponent(Component * comp);
void run();

private:
    Widget top_level;
    Widget pane;
    Component * components[10];
    int num_components;
    XtAppContext application_context;
};
```

`PaneWindow.cxx`文件中的`PaneWindow`类实现需要三个文件：前两个与`X`无关，第三个是类定义头文件：

```cpp
#include <X11/Intrins.h>
#include <X11/Xaw/Pane.h>
#include "PaneWindow.h"
```

为可能添加到分屏窗格的组件定义了以下`X`资源：

```cpp
static String app_resources[] = {
    "*TexteditType: edit",
    "*TextautoFill: on",
    "*TextscrollVertical: whenNeeded",
    "*TextscrollHorizontal: whenNeeded",
    "*TextpreferredPaneSize: 300",
    NULL,
};
```

如果你创建了`Component`的新子类来封装其他类型的控件，你可能想为`app_resources`数组中的这些控件类型添加默认资源。`PaneWindow`类构造函数创建了一个顶级应用程序（Top-Level Application）控件和一个`Athena`分屏窗格（`Athena Paned window`）：

```cpp
PaneWindow::PaneWindow() {
    int argc = 0;
    char ** argv = NULL;
    top_level = XtAppInitialize(&application_context, "top_level", NULL, 0,
        &argc, argv, app_resources,
        NULL, 0);
    num_components = 0;
    pane = XtVaCreateManagedWidget("paned", panedWidgetClass,
        top_level, NULL);
}
```

`run`方法创建已添加到`PaneWindow`的组件，然后处理`X`事件。类变量`num_components`是使用`addComponent`方法添加到此对象的组件数量的计数器：

```cpp
void PaneWindow::run() {
  // 开始添加所有注册的组件：
  for (int i=0; i<num_components; i++) {
    components[i]->getWidget();
  }
  XtRealizeWidget(top_level);
  XtAppMainLoop(application_context);
}
```

`addComponent`方法用于向`PaneWindow`对象中添加组件：

```cpp
void PaneWindow::addComponent(Component * comp) {
  components[num_components++] = comp;
}
```

# `Label`类（标签类）

`Label`类派生自`Component`类。类头文件`Label.hxx`只需要一个头文件，即其基类的定义文件：

```cpp
#include "Component.hxx"
```

类定义非常简单。构造函数接受三个参数，类私有数据使得`setup`方法在从`PaneWindow`对象的`run`方法中调用时能够正确创建标签：

```cpp
class Label : public Component {
public:
  Label(char * label = "test label", int width=100, int height=20);
  void setup(Widget parent);
private:
  char * my_label;
  int my_width;
  int my_height;
};
```

该类的实现也非常直观。`Label.c`文件需要四个包含文件，其中三个是`X Windows`特有的，一个定义了`Label`类：

```cpp
#include <X11/Intrinsic.h>
#include <X11/StringDefs.h>
#include <X11/Xaw/Label.h>
#include "Label.hxx"
```

类构造函数仅存储了它的三个参数，供`setup`方法以后使用：

```cpp
Label::Label(char *label, int width, int height) {
  my_label = label;
  my_width = width;
  my_height = height;
}
```

`setup`方法由`PaneWindow`对象的`run`方法调用；调用`setup`时传入了`PaneWindow`对象构造函数创建的`Athena Panel`控件。因此，添加的所有组件控件都将`Athena Panel`控件作为共同父：

```cpp
void Label::setup(Widget parent) {
  Arg args[2];
  XtSetArg(args[0], XtNwidth, my_width);
```
