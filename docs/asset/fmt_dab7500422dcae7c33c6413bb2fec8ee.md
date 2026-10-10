
### 22. 编写自己的小部件

#### 22.4.5 `gtk_dial_realize()`

现在我们来看某些类型的函数。首先，我们有一个执行创建 X 窗口任务的函数。注意，传递给 `gdk_window_new()` 函数的是一个掩码（mask），它指定了 `GdkWindowAtt` 结构中哪些字段包含数据（其余字段将具有默认值）。同样值得注意的是，这是小部件被创建时的的事件掩码。我们调用 `gtk_widget_get_events()` 来获取用户为此小部件指定的事件掩码（通过 `gtk_widget_set_events()` 设置），并添加我们感兴趣的事件。

创建窗口后，我们设置了它的样式和背景，并将窗口的指针存放在 `GdkWindow` 的用户数据（user data）中。最后最后一步允许 GTK 将该窗口的事件分发给正确的小部件。

```c
static void
gtk_dial_realize (GtkWidget *widget)
{
    GtkDial *dial;
    GdkWindowAttr attributes;
    gint attributes_mask;
    g_return_if_fail (dial != NULL);
    g_return_if_fail (GTK_IS_DIAL (dial));
    GTK_WIDGET_SET_FLAGS (widget, GTK_REALIZED);
    dial = GTK_DIAL (widget);
}
```

```c
attributes.x = widget->allocation.x;
attributes.y = widget->allocation.y;
attributes.width = widget->allocation.width;
attributes.height = widget->allocation.height;
attributes.wclass = GDK_INPUT_OUTPUT;
attributes.window_type = GDK_WINDOW_CHILD;
attributes.event_mask = gtk_widget_get_events (widget) |
GDK_EXPOSURE_MASK | GDK_BUTTON_PRESS_MASK |
GDK_BUTTON_RELEASE_MASK | GDK_POINTER_MOTION_MASK |
GDK_POINTER_MOTION_HINT_MASK;
attributes.visual = gtk_widget_get_visual (widget);
attributes.colormap = gtk_widget_get_colormap (widget);
attributes.mask = GDK_WINDOW_X | GDK_WA_Y | GDK_WA_VISUAL | GDK_WA_COLORMAP;
widget->window = gdk_window_new (widget->parent, attributes, attributes_mask);
widget->style = gtk_style_attach (widget->style, widget->window);
gdk_window_set_user_data (widget->window, widget);
gtk_style_set_background (widget->style, widget->window, GTK_STATE_ACTIVE);
}
```

#### 22.4.6 尺寸协商

在包含小部件的窗口首次显示之前以及每当窗口布局变化时，GTK 都会询问每个子部件其所需的尺寸。由于我们的小部件不是容器小部件，并且对其尺寸没有实际限制，我们只需返回一个合理的默认值。

```c
static void
gtk_dial_size_request (GtkWidget *widget,
GtkRequisition *requisition)
{
    requisition->width = DIAL_DEFAULT_SIZE;
    requisition->height = DIAL_DEFAULT_SIZE;
}
```

在窗口请求尺寸后，窗口的布局由 `gtk_dial_allocate()` 函数计算。注意，该实例可能比请求的尺寸小，但至少达到：

```c
static void
gtk_dial_allocate (GtkWidget *widget,
GtkAllocation *allocation)
{
    GtkDial *dial;
    g_return_if_fail (dial != NULL);
    g_return_if_fail (GTK_IS_DIAL (dial));
    dial = GTK_DIAL (widget);
}
```

```c
attributes.x = widget->allocation.x;
attributes.y = widget->allocation.y;
attributes.width = widget->allocation.width;
attributes.height = widget->allocation.height;
attributes.wclass = GDK_INPUT_OUTPUT;
attributes.window_type = GDK_WINDOW_CHILD;
attributes.event_mask = gtk_widget_get_events (widget) |
GDK_EXPOSURE_MASK | GDK_BUTTON_PRESS_MASK |
GDK_BUTTON_RELEASE_MASK | GDK_POINTER_MOTION_MASK |
GDK_POINTER_MOTION_HINT_MASK;
attributes.visual = gtk_widget_get_visual (widget);
attributes.colormap = gtk_widget_get_colormap (widget);
attributes.mask = GDK_WINDOW_X | GDK_WA_Y | GDK_WA_VISUAL | GDK_WA_COLORMAP;
widget->window = gdk_window_new (widget->parent, attributes, attributes_mask);
widget->style = gtk_style_attach (widget->style, widget->window);
gdk_window_set_user_data (widget->window, widget);
gtk_style_set_background (widget->style, widget->window, GTK_STATE_ACTIVE);
}
```

#### 22.4.7 `gtk_dial_expose()`

如上所述，小部件的绘制是在存储在样式中的处理函数中完成的。

```c
static int
gtk_dial_expose(GtkWidget *widget,
    GdkEvent *event)
{
    GtkDial *dial;
    GdkPoint points[3];
    double s, c;
    int xc, yc;
    int tick_length;
    int i;
    g_return_if_fail (dial != NULL);
    g_return_if_fail (GTK_IS_DIAL (dial));
    dial = GTK_DIAL (widget);
    gdk_window_clear_area(widget->window, 0, 0, allocation->width, allocation->height);
    xc = allocation->width/2;
    yc = allocation->height/2;
    /* 绘制刻度 */
    for (i=0; i<25; i++)
    {
        tick_length = (i%6 == 0) ? dial->pointer_width : dial->pointer_width/2;
        gdk_draw_line(widget->window,
            widget->style->gc,
```
