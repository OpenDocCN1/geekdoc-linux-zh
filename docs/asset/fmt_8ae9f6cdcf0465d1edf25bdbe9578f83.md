
```c
#include <gtk/gtk.h>

int main(int argc, char *argv[]) {

	GtkWidget *window;

		gtk_init (&argc, &argv);

	window = gtk_window_new (GTK_WINDOW_TOPLEVEL);

		gtk_widget_show (window);

		gtk_main ();

	return(0);

}
```

`gtk.h`头文件包含了GTK变量、宏和函数定义；`window`被定义为指向名为`GtkWidget`结构的指针。实际指向的结构将稍后由创建结构的函数确定。`gtk_init`函数创建初始设置，例如默认视觉和颜色映射，并调用`gdk_init`函数来初始化GTK库和GTK参数。`gtk_window_new`创建一个新的窗口结构，返回其地址，然后将其分配给`window`指针。`window`现在指向GTK窗口结构。`GTK_WINDOW_TOP_LEVEL`参数将窗口置于窗口管理器控制下，使用窗口管理器的默认值显示窗口。`gtk_widget_show`函数随后显示窗口——注意窗口指针被用作此函数的参数。最后，使用`gtk_main`函数运行控件。

以下`base.c`程序定义了一个简单的GTK程序，显示一个简单的：

某些对象具有与其关联的信号。

| Gnome 库函数类别 | 描述 |
|---|---|
| gnome-config | 提供对配置值的简单访问。 |
| gnome-defs | 包含用于 C++ 连接的 Gnome 定义。 |
| gnome-exec | 允许从 Gnome 应用执行程序。 |
| gnome-help | 包含显示帮助的例程。 |
| gnome-history | 跟踪最近使用的文档。 |
| gnome-i18n | 提供本地化和国际化支持。 |
| gnome-mime-info | 获取 MIME 类型信息的例程。 |
| gnome-paper | 包含纸张尺寸和单位转换。 |
| gnome-popt | 命令行参数解析器。 |
| gnome-regex | 包含正则表达式缓存实现。 |
| gnome-sound | 包括 Gnome 应用的声音例程。 |
| gnome-triggers | 包含应用程序事件的层级搜索机制。 |
| gnome-url | 允许根据 URL 启动文档查看器。 |
| gnome_lib | 初始化 gnome 库。 |

`libgnome`库包含了为应用程序创建Gnome用户界面所需的函数和结构，这些结构与GTK+控件集绑定，Gnome可以轻松地创建对话框和消息框，以及菜单栏、工具栏和状态行。为程序员提供了大量的库存图标，供其在对话框、菜单项和按钮中使用，由于所有Gnome应用都使用`libgnome`创建这些常用的GUI元素，因此视觉一致性得到了保证。在许多方面与Tk画布类似，Gnome画布为创建地址框、日历应用程序和电子表格提供了框架。

GUI应用需要大量使用图像来创建友好舒适的用户界面。传统上，将所有常用的图形格式加载到X11应用中非常困难。`libgtk`库通过提供强大的函数来加载多种文件格式（JPEG, GIF, TIFF, PNG, XP, PPM, PGM, PBM和BMP）解决了这个问题。文件被转换为内部24位RGB表示，并存在实用函数来缩放以及将RGB渲染为各种颜色深度（如果需要，带有抖动）。输入图像由`libgtk`内部缓存，以提高重复使用图像的应用程序性能。

## 信号与事件

要将特定事件与你想要的函数关联，你将使用`gtk_signal_connect`或`gtk_signal_connect_object`。当检测到信号时，相关的调函数将被调用并执行。

- *pressed* 当鼠标指针位于按钮上时按下了鼠标键
- *released* 当鼠标指针位于按钮上时释放了鼠标键
- *clicked* 当鼠标指针位于按钮上时，按按下并释放了鼠标键
- *enter* 鼠标指针移动到按钮上
- *leave* 鼠标指针移出按钮外

你也可以使用信号连接函数将事件直接连接到对象和函数，而不是使用信号。事件由X11服务器传输，用以指示诸如鼠标点击和菜单选择等发生的情况。使用`gtk_signal_connect`函数时，你使用的是事件名称而不是信号名称。回调函数包含一个额外的的事件参数。对于此参数，你可以使用`GdkEvent`或其他几种事件类型之一。这些列在表6中。

```c
void callback_func( GtkWidget *widget, GdkEvent *event, gpointer callback_data );
```

表6: 常用 GtkWidget 信号
| 事件类型 | GtkWidget 信号 |
| --- | --- |
| GDK_DELETE | "delete_event" |
| GDK_DESTROY | "destroy_event" |
| GDK_EXPOSE | "expose_event" |
| GDK_MOTION_NOTIFY | "motion_notify_event" |
| GDK_BUTTON_PRESS | "button_press_event" |
| GDK_2BUTTON_PRESS | "button_press_event" |
| GDK_3BUTTON_PRESS | "button_press_event" |
| GDK_BUTTON_RELEASE | "button_release_event" |
| GDK_KEY_PRESS | "key_press_event" |
| GDK_KEY_RELEASE | "key_release_event" |
| GDK_FOCUS_CHANGE | "focus_in_event", "focus_out_event" |
| GDK_SELECTION_CLEAR | "selection_clear_event" |
| GDK_SELECTION_REQUEST | "selection_request_event" |

例如，要将`button_press_event`与一个OK按钮关联，你会使用"`button_press_event`"作为信号名称。以下示例将按钮上的`button_press_event`与`button_press_callback`函数关联：

```c
gtk_signal_connect( GTK_OBJECT(button), "button_press_event", GTK_SIGNAL_FUNC(button_press_callback), NULL);
```

用于信号连接的回调函数（在此例中为`button_press_callback`）其事件参数将具有`GdkEventButton`类型。

```c
static gint button_press_callback( GtkWidget *widget, GdkEventButton *event, gpointer data );
```

以下示例将窗口Box关闭按钮的点击操作与`close-win`函数关联。该对象是`mywindow`，`delete_event`是关闭框事件，而`close-win`是程序员编写的函数，当此事件发生时执行其代码。当用户点击窗口的关闭框时，就会调用`close-win`函数。

```c
gtk_signal_connect (GTK_OBJECT (mywindow), "delete_event", GTK_SIGNAL_FUNC (close-win), NULL);
```
