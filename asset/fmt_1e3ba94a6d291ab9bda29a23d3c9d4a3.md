
`lower` 和 `upper` 参数定义了尺的范围，`max_size` 是将显示的最大数值。`position` 定义了指针指示器在尺子内的初始位置。

垂直尺子可以跨越 800 像素宽的窗口，因此：

```c
gtk_ruler_set_range( GTK_RULER(ruler), 0, 800, 800 );
```

尺子上的标记将从 0 到 800，每 100 像素有一个数字。如果我们让尺的范围从 7 到 16，我们将编写：

```c
gtk_ruler_set_range(GTK_RULER(ruler), 7, 16, 0, 20);
```

尺上的指示器是一个小三角形，指示指针相对于尺的位置。如果使用尺来跟踪鼠标指针，则应将 `motion_notify_event` 信号连接到 `motion_notify_event` 方法。为了跟踪窗口内所有的鼠标移动，我们将：

```c
#define EVENT_METHOD(i, x) GTK_WIDGET_CLASS(GTK_OBJECT(i))->class->x

gtk_signal_connect_object(GTK_OBJECT(area), "motion_notify_event",
  GtkSignalFunc)EVENT_METHOD(ruler, motion_notify_event),
  GTK_OBJECT(ruler) );
```

以下示例创建了一个绘制区域，上方有一个水平尺，左侧有一个垂直尺。绘制区域的尺寸为宽 600 像素、高 400 像素。水平尺跨越 7 到 13，每 100 像素有一个标记，而垂直尺跨越 0 到 400，每 100 像素有一个标记。绘制区域和尺的放置是通过表格完成的。

```c
/* example-start rulers .c */
#include <gtk/gtk.h>

#define EVENT_METHOD(i, x) GTK_WIDGET_CLASS(GTK_OBJECT(i))->class->x

#define XSIZE 600
#define YSIZE 400

/* 此程序在点击关闭按钮时获取控制权 */

void close_application( GtkWidget *widget, GtkEvent *event, gpointer data ) {
  gtk_main_quit();
}

/* 主程序 */

main(int argc, char *argv[]) {
  GtkWidget *window, *table, *area, *hrule, *vrule;

  /* 初始化 GTK 并创建主窗口 */
  gtk_init(&argc, &argv);
  window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
  gtk_signal_connect(GTK_OBJECT(window), "delete_event",
    GTK_SIGNAL_FUNC(close_application ), NULL);
  gtk_container_set_border_width(GTK_CONTAINER(window), 10);

  /* 为放置尺和绘制区域创建一个空间 */
  table = gtk_table_new(3, 2, FALSE);
  gtk_container_add(GTK_CONTAINER(table), table);

  area = gtk_drawing_area();
  gtk_drawing_area_size((GtkDrawingArea*)area, XSIZE, YSIZE);
  gtk_table_attach(GTK_TABLE(table), area, 1, 0, 2, 1);
  GTK_EXPAND(GTK_FILL, GTK_FILL, 0, 0);
  gtk_widget_set_events(area, GTK_POINTER_MOTION_MASK |
    GTK_POINTER_MOTION_HINT);

  /* 水平尺位于上方。当鼠标跨越
   * 绘制区域时，motion_event 将传递给
   * 尺的相应事件处理器。 */
  hrule = gtk_hrule_new();
  gtk_ruler_set_metric(GTK_RULER(hrule), GTK_PIXELS);
  gtk_ruler_set_range(GTK_RULER(hrule), 7, 13, 0, 20);
  gtk_signal_connect(GTK_OBJECT(area), "motion_event",
    GTK_SIGNAL_FUNC(method_handler),
    motion_event,
    GTK_RULER(hrule));

  /* 垂直尺位于左侧。当鼠标跨越
   * 绘制区域时，motion_event 将传递给
   * 尺的相应事件处理器。 */
  vrule = gtk_vrule_new();
  gtk_ruler_set_metric(GTK_RULER(vrule), GTK_PIXELS);
  gtk_ruler_set_range(GTK_RULER(vrule), 0, YSIZE, 10, YSIZE);
  gtk_signal_connect(GTK_OBJECT(area), "motion_event",
    (GtkSignalFunc)GTK_WIDGET_CLASS(GTK_OBJECT(vrule))->class)(
    motion_event,
    GTK_RULER(vrule));

  gtk_table_attach(GTK_TABLE(table), vrule, 0, 0, 1, 2);
  GTK_EXPAND(GTK_FILL), GTK_FILL, 0, 0);

  /* 显示所有内容 */
  gtk_widget_show( area );
  gtk_widget_show( hrule );
  gtk_widget_show( vrule );
  gtk_widget_show( table );
  gtk_widget_show( window );
  gtk_main();
  return(0);
  /* example-end */
```

### 9.8 状态栏

状态栏是用于显示文本消息的简单控件。它们保持着一个推入的消息栈，因此弹出当前消息将显示之前的文本消息。为了允许应用程序的不同部分使用同一个状态栏显示消息，使用状态栏标识符（Identifiers）来标识。消息按后进先出的顺序堆叠，而不是按标识符。一个状态栏通过调用以下函数创建：

```c
GtkWidget *statusbar_new( void );
```

通过调用带有短文本描述的以下函数请求一个新的标识符：

```c
guint gtk_statusbar_get_context_id( GtkStatus *statusbar,
const gchar *description );
```

有三个操作状态栏的函数：

```c
guint gtk_statusbar_push( GtkStatus *statusbar,
	int context_id,
	gchar *text );

void gtk_statusbar_pop( GtkStatus *statusbar)
	int context_id );

void gtk_statusbar_remove( GtkStatus *statusbar,
	int context_id,
	gchar *id );
```

第一个 `statusbar_push` 用于向状态栏添加新消息。它返回一个标识符，稍后传递给 `statusbar_remove` 函数以移除状态栏栈中指定的消息。`statusbar_pop` 函数移除栈中具有给定标识符的最高消息。以下示例创建了一个状态栏和两个用于向状态栏推入项目的按钮，以及一个用于弹出最后一个项目的按钮。

```c
/* example-start statusbar.c */
#include <gtk/gtk.h>
#include <glib.h>

GtkWidget *status_bar;
```

```c
void push_item(GtkWidget *widget, gpointer data) {
    static int count = 1;
    char buff[20];
    snprintf(buff, 20, "Item %d", count++);
    gtk_statusbar_push(GTK_STATUSBAR(status_bar), context_id, buff);
}

void pop_item(GtkWidget *widget, gpointer data) {
```
