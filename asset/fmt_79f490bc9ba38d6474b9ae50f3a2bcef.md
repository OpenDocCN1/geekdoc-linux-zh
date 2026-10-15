
```c
7:   GdkPixmap *icon_pixmap = NULL;
8:   GdkPixmap *icon_mask = NULL;
9:   GdkGC *pixmap_gc = NULL;
10:  GdkGC *mask_gc = NULL;
11:  GdkColor mask_color;
12: 
13:  /* 获取拖源组件的 GtkStyle。 */
14:  gtk_widget_ensure_style(widget);
15:  style = gtk_widget_get_style(widget);
16: 
17:  /* 计算拖动图标的几何形状。 */
18:  width = gdk_string_width(style->font, text) + 4;
19:  height = style->font->ascent + style->font->descent;
20: 
21:  /* 分配图标 pixmap 和掩码* */
22:  icon_pixmap = gdk_pixmap_new(window, width, height,
23:                              1);
24:  icon_mask = gdk_pixmap_new(NULL, width, height, 1);
25: 
26:  /* 初始化图标 pixmap 和图形
27:  上下文 * */
28:  pixmap_gc = gdk_gc_new(icon_pixmap);
29:  gdk_gc_set_foreground(pixmap_gc, &style->white);
30:  gdk_gc_set_background(pixmap_gc, &style->black);
31:  gdk_gc_set_function(pixmap_gc, GDK_COPY);
32:  gdk_gc_set_font(pixmap_gc, style->font);
33: 
34:  mask_gc = gdk_gc_new(icon_pixmap);
35:  mask_color.pixel = 1;
36:  gdk_gc_set_foreground(mask_gc, &mask_color);
37:  gdk_gc_set_function(mask_gc, GDK_COPY);
38: 
39:  /* 绘制拖动图标背景 */
40:  gdk_gc_set_foreground(mask_gc, &style->white);
41:  gdk_draw_rectangle(icon_pixmap, pixmap_gc, TRUE, 0, 0,
42:                     width, height);
43:  gdk_gc_set_foreground(mask_gc, &style->black);
44: 
45:  /* 让图标完全不透明。 */
46:  gdk_draw_rectangle(icon_mask, mask_gc, TRUE, 0, 0,
47:                      width, height);
48:  mask_color.pixel = 0;
49:  gdk_gc_set_foreground(mask_gc, &mask_color);
50: 
51:  /* 在图标 pixmap 中绘制文本。 */
52:  gdk_draw_text(icon_pixmap, style->font, pixmap_gc, 2,
53:                 style->ascent, strlen(text));
54: 
55:  /* 设置新图标。 */
```

# 实现拖放功能

```c
56: gtk_drag_set_icon_pixmap(drag_context),
57:     gdk_colormap_get_system(), icon_pixmap, icon_mask,
58:     width/2, height/2);
59: }
60: 
61: void drag_begin_handler(GtkWidget *widget,
62:     GtkDragContext *drag_context, gpointer user_data)
63: {
64:     /* 包含每个目标数据（target_data）
65:     数据的指针数组。 */
66:     gpointer *target_data = NULL;
67: 
68:     /* 指向提供的每个数据格式的临时
69:     句指针。 */
70:     gchar *html = NULL;
71:     gchar *string = NULL;
72:     time_t now = time(NULL);
73:     gchar *now_string = ctime(&now);
74: 
75:     g_print("S: Drag begin!");
76: 
77:     /* 绘制一个包含当前时间的拖动图标。 */
78:     draw_drag_icon(widget, drag_context, now_string);
79: 
80:     /* 为目标数据分配指针数组。 */
81:     target_data = g_new(gpointer, ntargets);
82:     gtk_object_set_data(GTK_OBJECT(widget), "target_data",
83:         target_data);
84: 
85:     /* 定义目标数据的内容。 */
86:     html = g_strcat("<P>It's <B>", now_string,
87:         "</B></P>", NULL);
88:     string = g_strcat("It's now ", now_string, ".", NULL);
89: 
90:     /* 复制目标数据并将其存储在数组的
91:     正确位置。 */
92:     target_data[TEXT_HTML] = g_strdup(html);
93:     target_data[STRING] = g_strdup(string);
94: }
```

# 验证目标位置

为了验证目标组件是否可以接受释放，当鼠标在拖放事件期间移动到其上方时，必须通知它。为了实现这一点，应该为目标组件连接 `drag_motion` 信号。处理函数的原型如下：

```c
boolean drag_motion_handler(GtkWidget *widget, GtkDragContext *context, gint x, gint y, guint time, gpointer user_data);
```

![](img/7fa99a9d28ad33fa75eb9)

`drag_motion` 信号处理器的参数为：

| 参数 | 描述 |
| :--- | :--- |
| `widget` | 接收信号的组件。 |
| `context` | 指向对应拖放事件的 `GdkDragContext` 结构。 |
| `x` | 鼠标相对于目标组件的 x 坐标。 |
| `y` | 鼠标相对于目标组件的 y 坐标。 |
| `time` | 事件发生的时间。 |
| `user_data` | 连接到组件时提供的可选用户数据。 |

当组件不是拖放目标时，函数返回 `FALSE`，此时应该检查其父组件。当返回 `TRUE` 时，该组件被视为拖放目标，你必须验证它是否可以接受释放。

这就是传递 `GdkDragContext` 结构的原因之一。它提供了检查目标是否为有效释放所需的所有信息。该结构定义如下：

```c
struct GdkDragContext {
  GdkProtocol protocol;
  gboolean is_source;

  GdkWindow *source_window;
  GdkWindow *dest_window;

  GList *targets;
  GdkAction actions;
  GdkAction suggested_action;
  GdkAction action;

  guint start_time;
};
```

在这种情况下，只有下面的成员是合适的：

## 实现拖放功能

| 成员 | 描述 |
| :--- | :--- |
| `targets` | 包含源组件支持的所有目标原子的 `GList`。你需要此列表来验证这些目标是否有是目标组件可以接受的。 |
| `actions` | 源组件支持的操作。 |
| `suggested_action` | 使用 `drag_begin()` 函数时由 GTK+ 自动建议的操作。这强制 Shift 和 Ctrl 修饰符对应默认操作。你可以从 `actions` 成员中选择任何操作，但这里提供的通常是最合理的。 |
