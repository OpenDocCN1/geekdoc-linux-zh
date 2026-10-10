
```c
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {

    gtk_main_quit();

    return(0);

}
```

这是一个非常简单的 GNOME 应用程序。在第 17 到 24 行中，系统被初始化，创建了一个窗口，并设置了用于关闭应用程序的回调。

第 26 到 31 行创建 `AgBargraph` 小部件，并立即向其插入五个柱状图。调用 `ag_bargraph_new()` 创建一个新的空小部件。每次调用 `ag_bargraph_add()` 都会通过提供名称和 0 到 100 之间的值来定义一个新条以显示。

第 33 行调用 `gtk_container_add()`，该函数将小部件插入窗口的容器。调用 `gtk_widget_show_all()` 会实现树中的所有小部件，包括 `AgBargraph` 小部件。

## AgBargraph 头文件

每个小部件都有自己的头文件，用于定义随小部件包含的结构、常量和函数。使用小部件的应用程序程序和小部件本身的 C 源代码都包含相同的头文件。以下是 `AgBargraph` 小部件的头文件。

```c
/* agbargraph.h */

#ifndef __AG_BARGRAPH_H

#define __AG_BARGRAPH_H

#include <gtk/gtk.h>

#include <gtk/gtkwidget.h>

#ifdef __cplusplus

extern "C" {

#endif

#define AG_BARGRAPH(obj) \
GTK_CHECK_CAST(obj,ag_bargraph_get_type(),AgBargraph)

#define AG_BARGRAPH_CLASS(klass) GTK_CHECK_CLASS_CAST( \
klass,ag_bargraph_get_type(),AgBargraphClass)

#define AG_IS_BARGRAPH(obj) \
GTK_CHECK_TYPE(obj,ag_bargraph_get_type())

typedef struct _AgBargraph AgBargraph;

typedef struct _AgBargraphClass AgBargraphClass;

typedef struct _AgBargraphBar AgBargraphBar;

struct _AgBargraph {

GtkWidget widget;

GdkColor *outside_color;

GdkColor *inside_color;

gint maximum_value;

gint bar_count;

gboolean contains_pointer;

AgBargraphBar *bars;

gchar *show_text;

GdkFont *text_font;

};

struct _AgBargraphClass {

GtkWidgetClass parent_class;

};

struct _AgBargraphBar {

gchar *name;

gint value;

GdkGC *gc;

gint x_right;

gint x_left;

};

#define AG_BARGRAPH_MAXIMUM 100

GtkWidget *ag_bargraph_new(void);

guint ag_bargraph_get_type(void);

void ag_bargraph_add(AgBargraph *agbargraph, gchar *name, gint value);

#ifdef __cplusplus

};

#endif

#endif /* __AG_BARGRAPH_H */
```

第 3、4 和 59 行上的预处理器条件语句可防止头文件被意外多次包含。由于此小部件使用 `*GtkWidget*` 作为其父类型，因此有必要包含 `*gtk.h*` 和 `*gtkwidget.h*`——正如在第 6 和 7 行所做的那样。之所以可以在 C++ 程序中使用此小部件，是因为编译器已被告知，第 10 和 57 行大括号之间的所有内容都应编译为 C 而非 C++。C++ 编译器总是定义 `__cplusplus`。

在第 13 行定义的宏 `AG_BARGRAPH` 尝试将指针转换为 `AgBargraph` 小部件指针——如果指针类型错误，转换将失败并发出错误消息。同样，在第 15 行定义的宏 `AG_BARGRAPH_CLASS` 将指针转换为 `AgBargraphClass` 指针。在第 17 行定义的宏 `AG_IS_BARGRAPH` 根据传递给它的对象是否为 `AgBargraph` 小部件返回 `TRUE` 或 `FALSE`。

您可以在第 20 到 22 行的 `typedef` 语句中看到更多的命名约定。结构体以 leading underscore（前导下划线）定义，然后使用 `typedef` 来分配名称。使用 `typedef` 定义结构体名称的优点是允许声明如下形式：

```c
AgBargraph *bargraph;
```

`AgBargraph` 的结构体在第 24 到 34 行定义。在第 25 行，`AgBargraph` 结构体顶部的第一件事是一个 `GtkWidget` 结构体。这意味着指向 `AgBargraph` 结构体的指针也可以创建为指向 `GtkWidget` 结构体的指针——这两个结构体从相同的地址开始。这就是为什么指向 `AgBargraph` 的指针可以转换为指向 `GtkWidget` 的指针。`GtkWidget` 结构体的顶部是这样声明的：

```c
struct GtkWidget {
  GObject;
  guint16 private_flags;
  ...
};
```

由于 `GtkWidget` 结构体中的第一件事是 `GObject`，因此这三种类型共享相同的起始地址。这意味着 `AgBargraph` 指针可以转换为 `GtkWidget` 指针或 `GObject` 指针，任何 `GtkWidget` 指针都可以转换为 `GtkWidget` 指针或 `GObject`。这种技术在 GTK+ 和 GNOME 的所有对象中都被使用；它们的共同父对象是 `GObject`。`GObject` 是所有其他对象的父类，或祖类——它不继承自任何其他对象。

在第 26 到 33 行定义的字段是 `AgBargraph` 小部件单个实例特有的。例如，每次向小部件添加新条时，`bar_count` 值都会递增，因此对于每个 `AgBargraph` 实例，它可能具有不同的值。将所有变量信息存储在单个结构体中的这种技巧使得创建和管理多个实例变得非常容易。第 36 行的类结构体 `_AgBargraphClass` 持有任何为整个对象类定义的字段，而不是仅为单个实例定义。例如，在第 33 行定义的 `text_font` 可用于独立地为每个 `AgBargraph` 实例设置字体。如果 `text_font` 字段包含在类结构体中，那么改变它一次就会将更改应用于小部件的所有实例。在此示例中，`AgBargraphClass` 结构体仅包含其父类的类结构体。

第 40 行的结构体 `_AgBargraphBar` 包含定义单个条所需的数据。每次向小部件添加新条时，都会将此类型的结构体添加到第 31 行名为 `bars` 的数组中。

函数原型在第 50 到 53 行定义。这些是非静态函数——应用程序调用的函数。始终至少有一个“new”函数以便创建对象，以及一个“type”函数以便通过唯一的类型 ID 号识别对象。通常，还有几个其他函数可用于控制小部件。在此示例中，唯一的自定义函数是 `ag_bargraph_add()`，它向小部件添加一个新的条。一些函数可以设计为对整个类进行操作，而另一些则对一个特定实例进行操作。针对特定实例操作的函数以其第一个参数作为小部件指针（以便函数知道要对哪个实例进行操作），而类级函数不需要这样的指针，因为其操作适用于整个类。

## AgBargraph 小部件

以下是 `AgBargraph` 小部件 C 源代码的描述。

虽然没有强制要求，但所有小部件似乎都是作为一个单一的源代码文件编写的。由于同一个文件既用于公共函数也用于私有函数，因此应将私有函数声明为 `static`（静态），以防止应用程序直接调用它们。由于静态函数只能在单个源文件内部被引用，最好将所有代码包含在一个文件中，以便静态函数可以从其他任何函数调用。源文件以 `#include` 文件和静态函数的原型开始。

以下列表比其他示例稍大且复杂，因此我将其拆分为各个部分，并分别描述每一部分。

```c
1 /* agbargraph.c */

2

3 #include "agbargraph.h"

4

5 #include <stdio.h>

6 #include <stdlib.h>

7

8 static void ag_bargraph_class_init(AgBargraphClass *klass);
```
