
# 显示显示按钮所有可能的状态。唯一不适用的是 SELECTED（已选中）状态。

```
fg[PRELIGHT] = { 0, 1.0, 1.0 }

bg[PRELIGHT] = { 0, 0, 1.0 }

bg[ACTIVE] = { 1.0, 0, 0 }

fg[ACTIVE] = { 0, 1.0, 0 }

bg[NORMAL] = { 1.0, 0, 0 }

fg[NORMAL] = { .99, 0, .99 }

bg[INSENSITIVE] = { 1.0, 1.0, 1.0 }

fg[INSENSITIVE] = { 1.0, 0, 1.0 }

}
```

# 在此示例中，我们继承了 "button" 式的属性，然后在创建新的 "main-button" 样式时覆盖字体和背景颜色。

```style
style "main_button" = "button"
{
font = "adobe-helvetica-medium-r-normal--*-*-s*-s*-*-100--*-*-s*-s*-*"
bg[PRELIGHT] = { 0.75, 0, 0 }
}
```

```style
style "toggle_button" = "button"
{
fg[NORMAL] = { 1.0, 0, 0 }
fg[ACTIVE] = { 1.0, 0, 0 }
# 这将 toggle_button 的背景位图设置为父控件的（如在应用程序中定义）
bg_pixmap[NORMAL] = "<parent>"
}
```

```style
style "text"
{
bg_pixmap[NORMAL] = "marble.xpm"
fg[NORMAL] = { 1.0, 1.0, 1.0 }
}
```

```style
style "ruler"
{
font = "adobe-helvetica-medium-r-normal--*-*-s*-s*-*-80--*-*-s*-s*-*"
}
```

## 22. 编写你自己的控件

```
# pixmap 路径 "./pixmaps"
```

# 这些设置控件类型以使用上面定义的样式。控件类型列在类层次结构中，但可能也可以列在本文中供用户参考。

```widget
widget_class "GtkWindow" style "window"
widget_class "GtkDialog" style "window"
widget_class "GtkFileSelection" style "window"
widget_class "Gtk+Scale" style "scale"
widget_class "GtkCheckButton" style "toggle-button"
widget_class "GtkRadioButton" style "toggle-button"
widget_class "GtkButton" style "button"
widget_class "GtkRuler" style "ruler"
widget_class "GtkText" style "text"
```

# 这将所有作为 "main window" 的子元素的按钮设置为 main_button 样式。这些必须被记录以便能够利用。
`widget main window.GtkButton* style "main_button"`

### 22.1 概述

尽管 GTK 分发版包含了许多类型的控件，应该涵盖了大多数基础需求，但可能会有那么时刻，你需要创建自己的控件类型。由于 GTK 广泛使用控件继承，并且已经有一个与你的需求非常接近的控件，因此只需几行代码就可以创建一个非常有用的新控件类型。但在编写新控件之前，请先检查一下，确保已经有人写过它。这可以防止重复劳动，并将 GTK 控件的数量保持在最少，这有助于保持不同应用程序代码和界面的一致性。作为此的另一面，当你完成控件后，请向世界宣布它，这样其他人也能受益。这样做最好的地方可能是 `gtk-list`。

示例的完整源代码可以在你获取本教程的地方，或从这里获取： `://www.gtk.org/~ataylor/gtk/tutorial/`

### 22.2 控件的特殊性

为了创建一个新控件，理解 GTK 对象如何工作至关重要。本节只是一个简短的概述。详情请参见参考文档。

GTK 控件是以面向对象的方式实现的。然而，它们是用 C 语言实现的。与使用 C++ 编译器相比，这大大提高了可移植性和稳定性；但这意味着控件编写者必须注意实现细节。一个类的所有实例的公共信息（例如，所有 `Button` 控件）存储在类结构中。关于该类的信息只有一份副本，存储在类中（作用类似于 C++ 中的虚函数）。为了支持继承，类结构中的第一个字段必须是父类类结构的副本。`GtkButton` 类结构的声明如下：

```c
struct _GtkButtonClass {
nGtkContainerClass parent_class;
};
```

```c
void (*pressed)(GtkButton *button);
void (*released)(GtkButton *button);
void (*clicked)(GtkButton *button);
void (*enter)(GtkButton *button);
void (*leave)(GtkButton *button);
```

当 GTK 控件被视为容器时，其类结构可以转换为 `GtkClass`。此外，一个结构用于存储每个实例不同的信息。对于该类的，`GtkButton` 类结构看起来如下：

```c
struct _GtkButton {
  GtkContainer *container;
  guint in;
  guint down;
};
```

注意，对于该类结构，第一个字段是父类的。

### 22.3 创建复合控件

#### 22.3.1 引言

你可能感兴趣的控件类型仅仅是其他控件的聚合。这种类型的控件不需要创建新的控件就能完成，但提供了一种方便的复用方式。GTK 分发版中的示例是这种类型的控件。

#### 22.3.2 选择父类

复合控件的父类通常是 `Dialog` 类。遗憾的是，这看起来很自然。控件的创建被在两个函数之间：一个调用用户的 `new()` 函数，另一个 `init()` 函数来初始化控件。这种分工对于需要知道行和列的 `table` 效果并不好。除非我们重复 `gtk_table()` 的功能。这是一个 3x3 的网格，当所有对角线被按下时，会触发信号。

#### 22.3.3 头文件

每个控件类都有一个头文件，声明该控件的对象和类结构，以及公共函数。几个特征值得注意。为了防止重复定义，我们将整个头文件封装在：

```cpp
#ifndef __CTAOE_H__
#define __CTAOE_H__
...
#endif /* __CTAOE_H__ */
```

为了让包含头文件的 C++ 程序开心，在：

```cpp
#ifdef __cplusplus
extern "C" {
#endif /* __cplusplus */
...
#ifdef __cplusplus
}
#endif /* __cplusplus */
```

与函数和结构一起，我们在头文件中声明了三个标准宏 `TICTOE(obj)`、`TOE_CLASS(klass)` 和 `IS_TACTOE(obj)`，它们分别是指向对象或类结构的指针，并检查一个对象是否是 `Tactoe` 控件。

这里是完整的头文件：

```cpp
/* tactoe.h */
#ifndef __CTAOE_H__
#define __CTAOE_H__
#include <gdk/gdk.h>
#include <gtk/gtkvbox.h>
#ifdef __cplusplus
extern "C" {
#endif /* __cplusplus */
#define TICTOE(obj) GTK_CHECK_CAST(obj, tactoe_get_type (), Tactoe)
#define TOE_CLASS(klass) GTK_CHECK_CLASS_CAST(klass, tactoe_toe_get_type (), Tactoe)
#define IS_TACTOE(obj) GTK_CHECK_TYPE(obj, tactoe_get_type ())
typedef struct _Tactoe Tactoe;
typedef struct _TactoeClass TactoeClass;
struct _Tactoe {
  GtkVbox vbox;
};
```

## 22. 编写自己的小组件

```c
GtkWidget *buttons[3][3];
};
```

```c
struct _TictactoeClass {
```
