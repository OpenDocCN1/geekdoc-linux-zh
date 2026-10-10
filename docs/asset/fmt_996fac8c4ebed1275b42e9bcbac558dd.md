
* 当窗口变为可见或
* `gdk_widget_draw` 程序被调用时，此
* 程序会被调用。将背景 `pixmap`
* 复制到窗口。
*/

`gint` `expose_event`(GtkWidget *widget, GdkEventExpose *event)
{
    /* -- 将 pixmap 复制到窗口 -- */
    `gdk_draw_pixmap`(widget->window,
                     widget->style->fg_gc[GTK_WIDGET_STATE(widget)],
                     `pixmap`,
                     event->area.x, event->area.y,
                     event->area.x, event->area.y,
                     event->area.width, event->area.height);
    return FALSE;
}

# 简单时钟应用程序 227

```c
/*
* quit
* 退出应用程序
*/
void quit ()
{
    gtk_exit (0);
}
```

```c
/*
* main
* 程序从这里开始。
*/
int main (int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *drawing_area;
    GtkWidget *vbox;
    gtk_init (&argc, &argv);
    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
    gtk_container_add (GTK_CONTAINER (window), vbox);
    gtk_widget_show (vbox);
    gtk_signal_connect(GTK_OBJECT (window), "destroy",
                        GTK_SIGNAL_FUNC (quit), NULL);
    /* -- 创建绘制区域 -- */
    drawing_area = gtk_drawing_new (window);
    gtk_drawing_area_size (GTK_DRAWING_AREA (drawing_area), 200, 200);
    gtk_box_pack_start (GTK_BOX (vbox), drawing_area, TRUE, TRUE, 0);
    gtk_widget_show (drawing_area);
    /* -- 处理 pixmap 的信号 -- */
    gtk_signal_connect(GTK_OBJECT (drawing_area), "expose_event",
                        (GtkSignalFunc) expose_event, NULL);
    gtk_signal_connect(GTK_OBJECT (drawing_area),"configure_event",
                        (GtkSignalFunc) configure_event, NULL);
    /* -- 显示窗口 -- */
    gtk_widget_show (window);
```

```c
/* --- 每秒重绘一次 --- */
gtk_timeout_add(1000, Repaint, drawing_area);
/* --- 调用主循环 --- */
gtk_main();
return 0;
}
```

## 系统监控器

我们将复用之前的一些代码来创建一个小型程序，监控机器并显示 CPU 和以太网连接的状态图（见图 10.4）。唯一的问题是如何获取关于系统的信息。![](img/0c259d8fa983d9a117943feedd0.png) 图10.4 系统监控。

### 使用 /proc 文件

关于 Linux 的许多信息可以从 `/proc` 文件获取。`proc` 目录下的“文件”可以像普通文件一样打开并解析，并提供大量关于机器的信息。例如，`proc/loadavg` 文件包含 CPU 信息。如果你对其他文件好奇，可以输入 `man proc` 来获取 `proc` 中所有文件的摘要。如果你查看 `/proc/loadavg`，会得到如下的内容：

```bash
0.00 0.00 0.00
```

前三个数字是过去 1 分钟、5 分钟和 15 分钟的平均负载。如果你在提示符中使用 `w` 命令，会得到类似：

```bash
4:15 up 3:34, 4 users, load average: 0.00, 0.00
```

上一行显示了平均负载（机器似乎是空闲的）。另一个 `/proc/net/dev` 文件包含了每个设备发送和接收数据包的信息。在我的机器上，结果如下：

| 接收 | 发送 |
| :--- | :--- |
| 丢弃帧 | 丢弃帧 |
| lo: | 103 0 | 103 0 |
| eth0: | 9639 0 0 | 6513 0 1 |

当然，发送和接收的数据包每次都会变化。稍后我输入命令，得到：

| 接收 | 发送 |
| :--- | :--- |
| 丢弃帧 | 丢弃帧 |
| lo: | 104 0 | 104 0 |
| eth0: | 9639 0 0 | 6513 0 1 |

我想监控的设备是 `eth0`：这是我机器上的以太网卡，我想知道任何时间通过网卡的流量。通过将总流量与上次读取文件进行比较，我可以确定上次读取文件以来产生了多少流量。

## 描述

应用程序使用定时器每几秒更新一次屏幕。它读取 `/proc` 文件系统统计信息，并在图中显示信息，图中每个项目都有不同的颜色。图表可以使用工具栏进行配置。

通过实验，我发现网络使用往往会波动，难以判断实际吞吐量。添加一个按钮显示平均吞吐量以及实际吞吐量更容易。平均值是通过最后 N 个样本计算的，提供的图表波动较小。

系统监控器的代码被分为几个模块。每个模块都有处理其部分的特定代码。文件的描述从 `frontend.c` 开始。`frontend.c` 创建应用程序窗口、工具栏（带有 `pixmap`）和小型菜单。它包含其他查询用户界面信息的函数。例如，可以调用 `CPUButton15Down` 来询问显示 15 分钟 CPU 状态的工具按钮是否被按下。这种方法比允许 `tool_cpu15` 变量在文件外使用更好（C语言的数据封装）。注意工具按钮颜色是不同的。工具栏中每个显示的颜色将与图中项目的颜色相同，方便用户开启或关闭项目。视觉颜色提示有助于建立图表与其工具栏按钮之间的关联。

```c
/*
 * 示例 GUI 应用程序前端。
* 作者: Eric Harlow
* 文件: frontend.c
*/
```

```c
#include <sys/stat.h>
#include <unistd.h>
#include <errno.h>
#include <gtk/gtk.h>
```

```c
/*
* --- 函数原型
*/
```

```c
GtkWidget *CreatedDrawingArea();
static void CreateMainWindow();
void CreateToolbar(GtkWidget *vbox_main);
void SetToolbarButton(char *szButton, int nState);
void SelectMenu(GtkWidget *widget, gpointer data);
void DeSelectMenu(GtkWidget *widget, gpointer data);
void SetMenuButton(char *szButton, int nState);
GtkWidget *CreateWidgetFromIcon(GtkWidget *window, gchar **xpm_data);
GtkWidget *CreateMenuItem(GtkWidget *menu,
char *szName,
char *szAccel,
char *szTip,
GtkSignalFunc func,
gpointer data);
GtkWidget *CreateMenuCheck(GtkWidget *menu,
char *szName,
GtkSignalFunc func,
gpointer data);
GtkWidget *CreateSubMenu(GtkWidget *menubar, char *szName);
