
```c
#include <gtk/gtk.h>

/* 用于绘图区域的底层 pixmap */
static GdkPixmap *pixmap = NULL;

/* 创建一个合适尺寸的新底层 pixmap */
static int
configure_event(GtkWidget *widget, GdkEventConfigure *event)
{
    if (pixmap)
        gdk_pixmap_unref(pixmap);

    pixmap = gdk_pixmap_new(widget->window,
                             widget->allocation.width,
                             widget->allocation.height,
                             -1);

    gdk_draw_rectangle(pixmap,
                       widget->style->white_gc,
                       TRUE,
                       0,
                       0,
                       widget->allocation.width,
                       widget->allocation.height);

    return TRUE;
}

/* 从底层 pixmap 重绘屏幕 */
static int
expose_event(GtkWidget *widget, GdkEventExpose *event)
{
    gdk_draw_pixmap(widget->window,
                    widget->style->fg_gc[GTK_WIDGET_STATE(widget)],
                    pixmap,
                    event->area.x, event->area.y,
                    event->area.width, event->area.height);

    return FALSE;
}

/* 在屏幕上画一个矩形 */
static void
draw_rectangle(GtkWidget *widget, double x, double y)
{
    update_rect.rect.x = x - 5;
    update_rect.y = y - 5;
    update_rect.width = 10;
    update_rect.height = 10;
    gdk_draw_rectangle (pixmap,
        widget->style->black_gc,
        update_rect.x, update_rect.y,
        update_rect.width, update_rect.height);
    gtk_widget_draw(widget, &update_rect);
}
```

```c
static gint
button_press_event(GtkWidget *widget, GdkEvent *event) {
    if (event->button == 1 && pixmap != NULL) {
        draw_brush(widget, event->x, event->y);
    }
    return TRUE;
}
```

```c
if (state & GDK_BUTTON1_MASK && pixmap != NULL) {
        draw_brush(widget, x, y);
    }
    return TRUE;
}
```

```c
void
quit () {
    gtk_exit (0);
}
int
main (int argc, char *argv[]) {
    GtkWidget *window;
    GtkWidget *drawing_area;
    GtkWidget *vbox;
    GtkWidget *button;
    gtk_init (&argc, &argv);
    window = gtk_window_new (GDK_WINDOW_TOPLEVEL);

    gtk_widget_set_name(window, "Test Input");

    vbox = gtk_bbox_new(FALSE, 0);
    gtk_container_add(GTK_CONTAINER (window), vbox);
    gtk_widget_show(vbox);
```

```c
gtk_signal_connect(GTK_OBJECT (window), "destroy",
GTK_SIGNAL_FUNC (quit), NULL;

/* 创建 drawing_area */
drawing_area = gtk_drawing_area();
gtk_widget_set_size(GTK_DRAWING_AREA (drawing_area), 200, 200);
gtk_box_pack_start(GTK_BOX (vbox), drawing_area, TRUE, 0);
gtk_widget_show(drawing_area);

/* 用于处理 pixmap 的信号 */
gtk_signal_connect(GTK_OBJECT (drawing_area), "expose_event",
(GtkSignalFunc)expose_event, NULL);
gtk_signal_connect(GTK_OBJECT (drawing_area), "configure_event",
(GtkSignalFunc)configure_event, NULL);

/* 事件信号 */
gtk_signal_connect(GTK_OBJECT (drawing_area), "motion_notify_event",
(GtkSignalFunc)motion_notify_event, NULL);
gtk_signal_connect(GTK_OBJECT (drawing_area), "button_press_event",
(GtkSignalFunc)button_press_event, NULL);
gtk_widget_set_events(drawing_area, GTK_EXPOSURE_MASK
| GTK_LEAVE_NOTIFY_MASK
| GTK_BUTTON_PRESS_MASK
| GTK_POINTER_MASK);

/* 以及一个退出按钮 */
button = gtk_button_new_with_label("Quit");
gtk_box_pack_start(GTK_BOX (vbox), button, FALSE, FALSE);
gtk_signal_connect(GTK_OBJECT (button), "clicked",
GTK_SIGNAL_FUNC (quit), NULL);

gtk_widget_show(button);
gtk_widget_show(window);

gtk_main();

return 0;
}
/* example-end */
```

## D List Widget

注意：`GtkList` 组件已被 `GTreeView` 组件取代。为了完整起见，在此列出它。`GtkList` 组件设计用于作为 `GtkListItem` 类型组件的垂直容器。`GtkList` 组件拥有它自己的接收事件的窗口和背景颜色（通常为白色）。由于它直接派自 `GtkContainer`，可以使用 `GTK_CONTAINER(List)` 宏进行处理。用户应该熟悉 `GList` 的用法及其相关函数 `g_list_*`，以便充分使用 `GtkList` 组件。

在 `GtkList` 组件的结构定义内部有一个我们感兴趣的字段：

```c
struct _GtkList
{
    GList *selection;
    guint selection_mode;
};
```

`selection` 字段指向所有选中项的链表，如果选择为空则指向 `NULL`。要了解当前选择，我们读取 `GtkList()->selection` 字段，但不要修改它，因为内部字段由 `gtk_list_*` 函数维护。

`GtkList` 的 `selection_mode` 决定了 `GtkList` 的选择机制，因此决定了 `GtkList()->selection` 字段的内容。选择可以是：

- `GTK_SELECTION_SINGLE` - 选择为 `NULL` 或包含单个选中项的 `GList` 指针。
