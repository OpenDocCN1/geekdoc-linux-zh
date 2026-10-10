
第 93 行响应 GDK_BUTTON_RELEASE 事件。对于这个程序，只有当释放的是左键（编号 1）时，释放事件才有意义，这表示绘图结束。如果是左键，状态会改变，以指示不再进行绘图。

> 这些事件相互之间相当独立。例如，你可以按住左键并拖动以绘制线条，同时点击右键以改变线条颜色。

第 101 行响应 GDK_2BUTTON_PRESS 事件。这就是双击。该程序唯一响应的双击是左键，它在第 105 行执行 gdk_draw_arc() 的调用，并在鼠标位置绘制一个实心圆。

第 113 行响应 GDK_3BUTTON_PRESS 事件。这就是三击。第 116 行的测试判断是否为中键（按钮 2）；如果是，则立即退出程序。

> 每当发生双击或三击时，单次事件也会被报告。也就是说，每当有 GDK_2BUTTON_PRESS 事件时，也会有 GDK_BUTTON_PRESS 和 GDK_BUTTON_RELEASE。后两者被称为“真实事件”，因为它们代表实际的硬件事件；而双击被称为“伪事件”，因为它由软件生成——它对两个真实事件的接近程度进行计时。三击的情况也是如此——按压和释放事件各有两个。

第 119 行响应 GDK_MOTION_NOTIFY 事件。每当鼠标移动时都会发出此事件。第 122 行检查当前状态，如果状态结构体中存在有效点，并且当前程序正在绘制线条，则会从旧点向新点绘制一条线。无论是否绘制线条，状态中的 x 和 y 值都会更新以反映新的鼠标位置。

第 133 行响应 GDK_EXPOSE 事件。当窗口的任何部分被揭示时，会发出此事件。实际应用通常重绘屏幕，但由于此程序没有费心保存必要的执行该操作的数据，因此屏幕被清除，并且模式被设置为指示没有点且没有绘图正在进行。

你可以使用此程序创建的那类显示效果的一个示例如图 12-1 所示。

## 捕获和释放鼠标

总会有这样的时刻，你的程序必须在继续之前从用户那里获得一些响应。为此，可以弹出一个窗口并捕获鼠标，在用户响应之前不释放。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_408_0.png)

**图 12-1：鼠标绘制圆圈和线条**

要捕获鼠标，窗口只需捕获所有来自鼠标的事件。捕获的第二部分（可选）是限制鼠标的移动。下面的程序是一个捕获鼠标、将光标更改为反映捕获状态并在点击按钮之前等待释放的示例。

```c
/** mousegrab.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
void grabMouse(GtkWidget *widget, GtkWidget *containWidget);
void ungrabMouse(GtkWidget *widget, gpointer data);

int main(int argc, char *argv[])
{
    GtkWidget *window;
    GtkWidget *box;
    GtkWidget *button;

    gnome_init("mousegrab", "1.0", argc, argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_container_set_border_width(GTK_CONTAINER(window), 30);
    gtk_signal_connect(GTK_OBJECT(window), "delete_event",
                       GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(window), "destroy",
                       GTK_SIGNAL_FUNC(eventDestroy), NULL);

    box = gtk_vbox_new(FALSE, 0);

    button = gtk_button_new_with_label("Grab Mouse");
    gtk_box_pack_start(GTK_BOX(box), button, FALSE, FALSE, 0);
    gtk_signal_connect(GTK_OBJECT(button), "clicked",
                       GTK_SIGNAL_FUNC(grabMouse), window);

    button = gtk_button_new_with_label("Ungrab Mouse");
    gtk_box_pack_end(GTK_BOX(box), button, FALSE, FALSE, 0);
    gtk_signal_connect(GTK_OBJECT(button), "clicked",
                       GTK_SIGNAL_FUNC(ungrabMouse), NULL);

    gtk_container_add(GTK_CONTAINER(window), box);
    gtk_widget_show_all(window);
    gtk_main();
    exit(0);
}

void grabMouse(GtkWidget *widget, GtkWidget *containWidget)
{
    GdkWindow *window = containWidget->window;
    GdkCursor *cursor = gdk_cursor_new(GDK_CROSSHAIR);
    gdk_pointer_grab(window,
                     TRUE,
                     (GdkEventMask)0,
                     window,
                     cursor,
                     GDK_CURRENT_TIME);
}

void ungrabMouse(GtkWidget *widget, gpointer data) {
    if(gdk_pointer_is_grabbed())
           gdk_pointer_ungrab(GDK_CURRENT_TIME);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
    if(gdk_pointer_is_grabbed())
           gdk_pointer_ungrab(GDK_CURRENT_TIME);
    gtk_main_quit();
    return(0);
}
```

第 26 行构建了一个垂直盒容器。第 28 行至 36 行创建了一对按钮，将它们添加到垂直盒中，并为每个按钮分配一个回调。捕获鼠标的回调名为 `grabMouse()`，释放鼠标的回调名为 `ungrabMouse()`。第 31 行对 `grabMouse()` 的连接使用主窗口作为传递给函数的数据。

从第 43 行开始的回调函数 `grabMouse()` 调用函数 `gdk_pointer_grab()` 以将鼠标的移动限制在指定窗口的矩形区域内。

第 45 行从作为数据指针传递给回调函数的 `GtkWidget` 中提取 `GtkWindow`。该窗口在第 47 行用作第一个参数，并在第 50 行再次用作第四个参数。第一个参数指定接收所有鼠标事件的窗口——在鼠标被捕获期间，无论鼠标位于何处，这都将是唯一能接收鼠标事件的窗口。再次将该窗口用作第四个参数（如本例中所示），将鼠标的移动限制在该窗口内。在这个示例中，两者都使用同一个窗口，因此鼠标指针无法离开捕获事件的窗口。

第 48 行的第二个参数设置为 `TRUE`，以便传入的事件从捕获窗口传播到其子窗口。在这个示例中，子窗口是两个按钮。如果将其设置为 `FALSE`，按钮将不会接收到任何鼠标事件，并且将没有方式取消捕获窗口。

> 总要给自己留一条出路。如果你捕获鼠标且程序没有释放它的方法，你就被困住了。即使杀掉程序关闭窗口也无法释放它——捕获在该窗口所在的矩形区域内仍然保持活动状态。X 服务器实际上执行捕获，它会保留鼠标捕获，直到收到特定命令将其释放。

第 49 行是事件掩码，指示要向捕获窗口发送哪些事件。在这个示例中，无需添加任何事件，因为已计划的事件将到达按钮（作为捕获窗口的子窗口），允许它们被点击。然而，如果你打算处理自己的事件，可以使用表 12-1 中显示的事件掩码的任意组合。例如，如果你想在任何鼠标按钮或键盘按键按下时接收通知，请使用此掩码值：

```
GDK_BUTTON_PRESS_MASK | GDK_KEY_PRESS_MASK
```

| 掩码 | 事件 |
| --- | --- |
| GDK_EXPOSURE_MASK | GdkEventExpose。窗口已被揭示，需要绘制。 |
| GDK_POINTER_MOTION_MASK | GdkEventMotion。鼠标已移动。 |
| GDK_POINTER_MOTION_HINT_MASK | 当与 GDK_POINTER_MOTION_MASK 一起使用时，减少事件数量。 |
| GDK_BUTTON_MOTION_MASK | GdkEventMotion。鼠标在按住一个或多个按钮的情况下移动。 |

（续）
