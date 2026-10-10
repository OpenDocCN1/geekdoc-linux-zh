
## 22.4 从零开始创建组件

### 22.4.1 引言

在本节中，我们将学习更多关于组件如何在屏幕上显示以及如何与元素交互的知识。作为一个示例，我们将创建一个带有指针的模拟拨盘组件，用户可以拖动指针到某个特定值。

### 22.4.2 在屏幕上显示组件

在屏幕上显示涉及多个许多工作。在调用 `WIDGETNAME_new()` 创建组件后，还需要后续几个函数：
- `WIDGETNAME_realize()` 负责为该组件创建一个 X 窗口（如果它有的话）。
- `WIDGETNAME_map()` 在用户调用 `gtk_widget_show()` 后被触发。它负责确保组件实际绘制在屏幕上（映射）。对于容器组件，它还必须调用任何子组件的 `map()` 函数。
- `WIDGETNAME_draw()` 被组件或其任一祖先调用。它实际调用绘图函数来在屏幕上绘制组件。对于容器组件，此函数必须为其没有自己窗口的子组件生成 `expose`（暴露）事件。（如果它们有自己的窗口，则 X 会生成 `expose` 事件）。
- `WIDGETNAME_expose()` 是组件的 `expose` 事件处理程序。它调用必要的绘图函数来绘制屏幕上被暴露的位置。对于容器组件，此函数必须为其子组件生成 `expose` 事件（如果它们有自己的窗口，则 X 会生成 `expose` 事件）。

你可能会注意到最后几个函数非常相似——每个函数都负责在屏幕上绘制组件。在许多类型的组件中，它们并不不在乎两者之间的区别。组件类中默认的 `draw()` 函数只需为重绘区域生成一个合成的 `expose`。然而，某些类型的组件可以通过区分这两个函数来节省工作。例如，如果一个组件有多个窗口，那么 `expose` 事件可以识别被暴露的窗口，从而只重绘受影响的组件，而 `draw()` 调用是无法做到这一点。

容器组件即使不在乎区别，也不能简单地使用 `draw()` 函数，因为它们的子组件可能在意这种区别。然而，在两个函数之间重复绘图代码是浪费的。做法是组件拥有一个名为 `WIDGETNAME_paint()` 的函数，它执行绘制组件的实际工作，然后由 `draw()` 和 `expose()` 函数调用。

在我们的示例方法中，拨盘组件不是容器组件，而只有一个窗口，我们可以采取最简单的方法，使用默认的 `draw()` 函数并实现一个 `expose()` 函数。

### 22.4.3 拨盘组件的起源

就像所有人类都是爬上陆地的第一种两栖动物的变体一样，Gtk 组件往往始于某些其他预先编写的组件的变体。拨盘组件真正始于 `Range` 组件的源代码。选择它作为起点是因为如果我们的拨盘具有与 `Scale` 组件相同的接口就太好了，而 `Scale` 只是 `Range` 组件的特化后代。因此，虽然代码代码以完成的形式呈在下方，但不应暗示我们是以这种方式使用了“机械天神”（deus ex machina）。此外，如果你不从应用程序的角度熟悉 `scale` 组件的工作原理，那么最好在继续之前先看看它们。

### 22.4.4 基础

我们的组件很大一部分在 `Tictact` 组件中看起来很熟悉。首先，我们有一个头文件：

```c
/* GTK The GIMP Toolkit
 * Copyright (C) 1996-1997 Peter Mattis, Spencer Kimball and Josh MacDonald
 * 此库是自由软件；你可以根据自由软件基金发布的 GNU 
 * 库通用许可证 (General Public License) 重新分发和/或
 * 修改它；该许可证的第 2 版本，或（根据你的选择）任何后续版本。
 *
 * 分发此库的目的是希望它是有用的，
 * 不提供任何保证；即使没有对于商品性或
 * 特定用途的适用性的暗示保证。详情请参阅 GNU 
 * 库通用许可证。
 *
 * 你应该收到一份随本库提供的 GNU 
 * 许可证副本；如果没有，请写信给
 * Software Foundation, Inc., 675 Mas Ave, Cambridge, MA 0139, USA.
 */

#ifndef __GTK_DIAL_H__
#define __GTK_DIAL_H__

#include <gdk/gtk.h>
#include <gtk/adjustment.h>
#include <gtk/gtkwidget.h>

#ifdef __cplusplus
extern "C" {
#endif /* __cplusplus
#define GTK_DIAL(obj) GTK_CHECK_CAST(obj, gtk_dial_get_type(), GtkDial)
#define GTK_DIAL_CLASS(klass) GTK_CHECK_CAST(klass, gtk_dial_get_type(), GtkDialClass)
#define GTK_IS_DIAL(obj) GTK_CHECK_TYPE(gtk_dial_get_type())

typedef struct _GtkDial GtkDial;
typedef struct _GtkDialClass GtkDialClass;

struct _GtkDial {
  GtkWidget widget;
  /* 更新策略 (GTK_UPDATE_ [CONTINUOUS/DELAYED/DISCONTINUOUS]) */
  guint policy : 2;
  /* 按钮按下或 0 表示无 */
  guint8 button;
  /* 拨盘组件的尺寸 */
  gint radius;
  gint pointer_width;
  /* 更新计时器的 ID，或 0 表示无 */
  guint32 timer;
  /* 当前角度 */
  gfloat angle;
  /* 存储调整的旧值以便知道何时变化 */
  gfloat old_value;
  gfloat old_lower;
  gfloat old_upper;
  /* 存储数据的调整对象 */
  GtkAdjustment *adjustment;
};

struct _GtkDialClass {
  GtkWidgetClass parentclass;
};

#ifdef __cplusplus
}
#endif /* __cplusplus */
#endif /* __GTK_DIAL_H__
```

## 22. 编写自己的小部件

```c
GtkWidget*
gtk_dial_new (GtkAdjustment *adjustment)
{
  GtkDial *dial;
  dial = gtk_type_new (gtk_dial_get_type());
  if (!adjustment)
    adjustment = (GtkAdjustment*) gtk_adjustment_new(0.0, 0.0, 0.0, 0.0, 0.0, 0.0);
  gtk_dial_set_adjustment(dial, adjustment);
  return GTK_WIDGET (dial);
}

static void
gtk_dial_destroy (GtkObject *object)
{
  g_return_if_fail (object != NULL);
  g_return_if_fail (GTK_IS_DIAL (object));
  dial = GTK_DIAL (object);
  if (dial->adjustment)
    gtk_unref (GTK_OBJECT (dial->adjustment));
  if (GTK_OBJECT_CLASS (parent_class)->destroy)
    (GTK_OBJECT_CLASS (parent_class)->destroy) (object);
}
```

注意，这个 `init()` 函数对 Tictao 小部件的作用较少，因为它不是一个复合小部件；而 `new()` 函数的作用更大，因为它现在有一个参数。此外，请注意当我们存储指向 `Adjustment` 对象的指针时，我们会增加它的引用计数（并在不再使用它时相应地减少，以便 Gtk 能够跟踪它何时可以安全地销毁）。

此外，还有管理小部件选项的方法：

```c
GtkAdjustment*
gtk_dial_get_adjustment (GtkDial *dial)
{
  g_return_if_fail (dial != NULL);
  g_return_if_fail (GTK_IS_DIAL (dial), NULL);
  return dial->adjustment;
}

void
gtk_dial_set_update_policy (GtkDial *dial,
```
