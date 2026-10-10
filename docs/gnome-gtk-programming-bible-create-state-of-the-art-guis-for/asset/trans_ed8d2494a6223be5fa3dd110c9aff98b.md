
20    GtkStyle *current;
21    GtkStyle *new;
22    GdkBitmap *mask;
23
24    gnome_init("stylemod", "1.0", argc, argv);
25    app = gnome_app_new("stylemod", "GtkStyle");
26    gtk_container_set_border_width(GTK_CONTAINER(app), 40);
27    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
28    GTK_SIGNAL_FUNC(eventDelete), NULL);
29    gtk_signal_connect(GTK_OBJECT(app), "destroy",
30    GTK_SIGNAL_FUNC(eventDestroy), NULL);
31
32    gtk_widget_show(app);
33
34    button = gtk_button_new_with_label("Button");
35    gtk_widget_set_usize(button, 100, 100);
36
37    current = gtk_widget_get_default_style();
38    new = gtk_style_copy(current);
39
40    new->bg[GTK_STATE_ACTIVE] = green;
41    new->bg[GTK_STATE_PRELIGHT] = red;
42    new->bg[GTK_STATE_NORMAL] = cyan;
43    new->bg_pixmap[GTK_STATE_NORMAL] =
44    gdk_pixmap_create_from_xpm_d(app->window,
45    &mask, &new->bg[GTK_STATE_NORMAL],
46    (gchar **)module);
47    gtk_widget_set_style(button, new);
48
49    gnome_app_set_contents(GNOME_APP(app), button);
50    gtk_widget_show_all(app);
51
52    gtk_main();
53    exit(0);
54    }
55    gint eventDelete(GtkWidget *widget,
56    GdkEvent *event, gpointer data) {
57    return(FALSE);
58    }
59    gint eventDestroy(GtkWidget *widget,
60    GdkEvent *event, gpointer data) {
61    gtk_main_quit();
62    return(0);
63    }

在第 24 到 30 行 GN0ME 环境初始化完成后，立即在第 32 行通过 `gtk_widget_show()` 调用顶层应用程序窗口。这种初始化是必要的，因为它创建了一个颜色映射（color map），并使设置小部件样式所需的信息可用。样式可以稍后设置——在所有小部件显示之后——但初始化允许我们在小部件显示之前对其进行配置。

第 34 行和第 35 行调用 `gtk_button_new_with_label()` 和 `gtk_widget_set_usize()` 来创建一个大型按钮。

第 37 行获取当前的默认 `GtkStyle`。这是应用于所有未拥有自身样式的小部件的样式。虽然可以创建一个全新的样式，但这意味着需要填充 `GtkStyle` 结构体的每个成员——更常规的做法是从默认样式开始并简单地进行修改。现在，由于 `gtk_widget_get_default_style()` 返回的是一个指针，且该指针被程序中的所有小部件共用，直接修改默认样式会改变应用程序中所有小部件的样式。我们需要修改它的副本，因此在第 38 行调用 `gtk_style_copy()` 来创建默认 `GtkStyle` 的精确副本。

在复制的 `GtkStyle` 结构体中，第 40 行到第 42 行分配用于指示激活（active）、预亮（prelight）和正常（normal）状态的颜色。这些颜色在第 12 行到第 14 行定义，无需显式分配这些颜色——每当 `GtkStyle` 添加到一个小部件时，它们会被自动分配。

第 43 行创建一个像素图（pixmap），并将其安装用于按钮处于正常状态时。`gdk_pixmap_create_from_xpm_d()` 的调用使用主应用程序小部件的窗口和颜色映射信息，以及包含在第 4 行中的像素图定义。像素图是为活动状态设置的，因此该状态的背景颜色在第 45 行提供给像素图创建函数。最终生成的按钮如图 14-3 所示。像素图远小于按钮，但它会被重复平铺并填充整个按钮区域。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_462_0.png)

### 图 14-3：显示像素图样式的按钮

新的样式信息通过在第 47 行调用 `gtk_widget_set_style()` 设置到小部件中。第 49 行和第 50 行将按钮添加到主窗口，并且对 `gtk_widget_show_all()` 的调用导致包含按钮的窗口得以显示。

前面的示例展示了如何为单个小部件分配样式。要对多个小部件应用特殊样式，你可以为每一个调用 `gtk_widget_set_style()`——或者你可以暂时设置默认样式。例如，以下代码使用一个新创建的 `GtkStyle` 对象来创建多个小部件：

```
current = gtk_widget_get_default_style();
new = gtk_style_copy(current);
/* Make modification to new style */
gtk_widget_push_style(new);
/* Create new widgets */
gtk_widget_pop_style();
```

调用 `gtk_widget_push_style()` 会用新样式替换默认样式，并保存现有样式；调用 `gtk_widget_pop_style()` 则恢复原样式。你可以使用此方法对一组小部件的外观进行特殊调整。并且，由于这是一个压入-弹出（push-pop）的情况，调整组内的小部件可以进行各自的调整。

如果你有一个已经修改过样式的小部件，并且需要创建另一个具有相同修改的小部件，请这样做：

```
style = gtk_widget_get_style(existingWidget);
gtk_widget_set_style(newWidget, style);
```

当然，如果你想进行进一步的修改，你需要处理一个副本，因为你对原始样式的任何修改也会影响现有小部件。

## 总结

在最低层面，每个可显示对象都是一个 `GtkWidget` 对象，并在程序中可如此处理。在小部件层面进行的设置会影响其后代（即该可显示对象）的显示和行为（任何父类中包含 `GtkWidget` 的对象都被称为小部件）。关于配置小部件，本章探讨了：

- 小部件有几种存在状态，范围从原始分配到屏幕显示。除非你需要做特殊的事情，否则小部件从一个状态到另一个状态的移动完全是自动的。
- 有一些信息可以检索，以便你的应用程序更了解小部件。对于容器小部件来说，了解包含小部件的几何信息特别有用。
- 小部件的样式——其颜色模式和字体——可以在任何时候为任何小部件设置。此外，这些设置可以从一个小部件复制到另一个小部件。

下一章讨论一种特殊类型的应用程序。它被称为*小工具*（applet），并将其主窗口作为按钮显示在 GNOME 面板上。它通常用于启动应用程序，但也有专用小部件。GNOME 系统菜单和时钟是两个专用小工具的示例。

## 小工具（Applets）

![](img/8bcc1ba72831c7d67cfc8b395deab95f_464_0.png)

小工具是一种具有一个特殊特性的 GNOME 应用程序——它将主窗口显示为 GNOME 桌面面板的成员。面板承担了定位和显示窗口的责任。编写小工具并不比编写 GNOME 应用程序更困难。结构大致相同——你调用一个初始化函数，创建要显示的小部件，并调用事件循环函数。小工具小部件和面板为你完成大部分工作。一旦小工具运行起来，你可以对它做任何正常应用程序可以做的事情。

- **本章内容**
  - 创建窗口位于面板内的小工具
  - 使用小工具启动应用程序
  - 使用小工具窗口在面板中显示数据
  - 调整小工具的大小和形状以适应面板方向
  - 向小工具菜单添加选项

### 简化的 Applet

以下示例展示了让 applet 工作所需的最少代码。这个 applet 所做的只是在面板上显示一个简单的按钮。

```
/** simple_applet.c **/
#include <gnome.h>
#include <applet-widget.h>

#define APPLETNAME "simple-applet"
#define VERSION "1.0"

int main(int argc, char *argv[])
{
    GtkWidget *applet;
    GtkWidget *button;

    applet_widget_init(APPLETNAME, VERSION,
                       argc, argv,
                       NULL, 0, NULL);

    applet =
    applet_widget_new(APPLETNAME);
    button =
    gtk_button_new_with_label("Simple\nApplet");
    gtk_widget_set_usize(button, 48, 48);
    applet_widget_add(APPLET_WIDGET(applet), button);
}
```

